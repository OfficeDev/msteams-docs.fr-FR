---
title: Modifications de l’API du bot pour les membres de l’équipe et de la conversation
author: ojasvichoudhary
description: Décrit les modifications à venir et en cours apportées aux API bot utilisées pour récupérer les membres des équipes et des conversations
keywords: Liste des membres de l’équipe des api bot Framework
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: dfa85832fe8225b58e4566ba889c23d2696807e4
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/09/2022
ms.locfileid: "64737208"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams modifications apportées à l’API de bot pour récupérer des membres d’équipe ou de conversation

>[!NOTE]
> Le processus de dépréciation et `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` les API ont commencé. Initialement, ils sont fortement limités à cinq demandes par minute et retournent un maximum de 10 000 membres par équipe. La liste complète n’est donc pas retournée à mesure que la taille de l’équipe augmente.
> Vous devez mettre à jour vers la version 4.10 ou ultérieure du Kit de développement logiciel (SDK) Bot Framework et basculer vers les points de terminaison d’API paginés ou l’API `TeamsInfo.GetMemberAsync` mono-utilisateur. Cela s’applique également à votre bot même si vous n’utilisez pas directement ces API, car les SDK plus anciens appellent ces API pendant les événements [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) . Pour afficher la liste des modifications à venir, consultez [les modifications d’API](team-chat-member-api-changes.md#api-changes).

Actuellement, si vous souhaitez récupérer des informations pour un ou plusieurs membres d’une conversation ou d’une équipe, vous pouvez utiliser les API `TeamsInfo.GetMembersAsync` [de bot Microsoft Teams](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) pour C# ou `TeamsInfo.getMembers` pour les API TypeScript ou Node.js. Pour plus d’informations, consultez [la liste d’extraction ou le profil utilisateur](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile).

Ces API présentent les lacunes suivantes :

* Pour les grandes équipes, les performances sont médiocres et les délais d’attente sont plus probables : la taille maximale de l’équipe a considérablement augmenté depuis Teams a été publiée au début de 2017. En tant que `GetMembersAsync` liste de membres entière ou `getMembers` retournée, l’appel d’API prend beaucoup de temps à revenir pour les grandes équipes, et il est courant que l’appel expire et vous devez réessayer.
* Il est difficile d’obtenir les détails du profil pour un seul utilisateur : pour obtenir les informations de profil d’un seul utilisateur, vous devez récupérer la liste des membres entière, puis rechercher celle souhaitée. Il existe une fonction d’assistance dans le Kit de développement logiciel (SDK) Bot Framework pour la simplifier, mais elle n’est pas efficace.

Avec l’introduction d’équipes à l’échelle de l’organisation, il est nécessaire de mieux aligner ces API sur Office 365 contrôles de confidentialité. Les bots utilisés dans les grandes équipes peuvent récupérer des informations de profil de base similaires à l’autorisation `User.ReadBasic.All` Microsoft Graph. Les administrateurs de locataires contrôlent considérablement les applications et les bots qui peuvent être utilisés dans leur locataire, mais ces paramètres sont différents de ceux de Microsoft Graph.

Le code suivant fournit un exemple de représentation JSON de ce qui est retourné par Teams API de bot :

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

Voici les prochaines modifications apportées à l’API :

* Une nouvelle API est créée [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) pour récupérer les informations de profil pour les membres d’une conversation ou d’une équipe. Cette API est désormais disponible avec le Kit de développement logiciel (SDK) Bot Framework version 4.8 ou ultérieure. Pour le développement dans toutes les autres versions, utilisez la [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) méthode.

    > [!NOTE]
    > Dans v3 ou v4, la meilleure action consiste à effectuer une mise à niveau vers la version la plus récente, 3.30.2 ou 4.8 ou ultérieure, respectivement.

* Une nouvelle API est créée [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) pour récupérer les informations de profil pour un seul utilisateur. Il prend l’ID de l’équipe ou de la conversation et un [UPN](/windows/win32/ad/naming-properties#userprincipalname) qui est `userPrincipalName`, Microsoft Azure Active Directory (Azure AD) ID d’objet, ou l’ID `objectId``id` d’utilisateur Teams comme paramètres et retourne les informations de profil pour cet utilisateur.

    > [!NOTE]
    > `objectId` est modifié pour correspondre à `aadObjectId` ce qui est appelé dans l’objet `Activity` d’un message Bot Framework. La nouvelle API est disponible avec la version 4.8 ou ultérieure du Kit de développement logiciel (SDK) Bot Framework. Il est également disponible dans l’extension Teams SDK Bot Framework 3.x. En attendant, vous pouvez utiliser le point de terminaison [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) .

* `TeamsInfo.GetMembersAsync` en C# et `TeamsInfo.getMembers` en TypeScript ou Node.js est formellement déconseillé. Une fois la nouvelle API disponible, vous devez mettre à jour vos bots pour l’utiliser. Cela s’applique également à [l’API REST sous-jacente utilisée par ces API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).
* À la fin de 2022, les bots ne peuvent pas récupérer de manière proactive les `userPrincipalName` propriétés `email` des membres d’une conversation ou d’une équipe. Les bots doivent utiliser les API Graph pour récupérer l’imformation requise. La nouvelle `GetConversationPagedMembers` API ne peut pas retourner les propriétés de `email` la `userPrincipalName` fin de 2022. Les bots doivent utiliser API Graph avec un jeton d’accès pour récupérer des informations. 
