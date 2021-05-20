---
title: Modifications de l’API du bot pour les membres de l’équipe et de la conversation
author: ojasvichoudhary
description: Décrit les changements à venir et en cours aux API Bot utilisés pour récupérer les membres des équipes et des chats
keywords: bot framework apis team members roster (en)
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 333a29664f0d60e89039f906fce77e71054d486f
ms.sourcegitcommit: 9ef3b415cbba484c2201abe9c6927e08d974388e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52555436"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams api bot pour aller chercher des membres de l’équipe ou du chat

>[!NOTE]
> Le processus de dévadation `TeamsInfo.getMembers` et `TeamsInfo.GetMembersAsync` les API ont commencé. Initialement, ils sont fortement étranglés à cinq demandes par minute et retournent un maximum de 10K membres par équipe. Il en résulte que l’effectif complet n’est pas retourné à mesure que la taille de l’équipe augmente.
> Vous devez mettre à jour la version 4.10 ou plus du SDK Bot Framework et passer aux paramètres paginés de l’API, ou à `TeamsInfo.GetMemberAsync` l’API utilisateur unique. Cela s’applique également à votre bot, même si vous n’utilisez pas directement ces API, comme les anciens SDK appellent ces API lors [d’événements membersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Pour afficher la liste des modifications à venir, voir [modifications de l’API](team-chat-member-api-changes.md#api-changes). 

Actuellement, les développeurs de bots qui souhaitent récupérer des informations pour un ou plusieurs membres d’un chat ou d’une équipe utilisent les API bot Microsoft Teams `TeamsInfo.GetMembersAsync` pour C# `TeamsInfo.getMembers` ou pour TypeScript ou Node.js API. Pour plus d’informations, consultez [la liste d’extraction ou le profil de l’utilisateur](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile). Ces API ont plusieurs lacunes.

Actuellement, si vous souhaitez récupérer des informations pour un ou plusieurs membres d’un chat ou d’une équipe, vous pouvez [utiliser les API bot Microsoft Teams](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) pour C# ou pour `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` typescript ou Node.js API. Ces API ont les lacunes suivantes :

* Pour les grandes équipes, les performances sont médiocres et les temps d’attente sont plus probables : la taille maximale de l’équipe a considérablement augmenté depuis la sortie de Teams début 2017. Comme `GetMembersAsync` ou `getMembers` retourne l’ensemble de la liste des membres, il faut beaucoup de temps pour l’appel API de revenir pour les grandes équipes, et il est fréquent pour l’appel de temps libre et vous devez essayer à nouveau.
* Il est difficile d’obtenir des détails de profil pour un seul utilisateur : pour obtenir les informations de profil d’un seul utilisateur, vous devez récupérer l’ensemble de la liste des membres, puis rechercher celle que vous voulez. Il y a une fonction d’aide dans le Bot Framework SDK pour le rendre plus simple, mais il n’est pas efficace.

Avec l’introduction d’équipes à l’échelle de l’organisation, il est nécessaire de mieux aligner ces API sur les contrôles Office 365 la vie privée. Les bots utilisés dans les grandes équipes sont en mesure de récupérer des informations de profil de base similaires `User.ReadBasic.All` à l’autorisation Graph Microsoft. Les administrateurs locataires ont un grand contrôle sur les applications et les bots qui peuvent être utilisés dans leur locataire, mais ces paramètres sont différents de ceux de Microsoft Graph.

Le code suivant fournit un exemple de représentation JSON de ce qui est retourné par Teams api bot :

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

* Une nouvelle API est créée pour [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) récupérer les informations de profil pour les membres d’un chat ou d’une équipe. Cette API est maintenant disponible avec la version Bot Framework 4.8 ou plus tard SDK. Pour le développement dans toutes les autres versions, utilisez la [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) méthode.

    > [!NOTE]
    > En v3 ou v4, la meilleure action est de passer à la dernière version de point qui est 3.30.2 ou 4.8 ou plus tard respectivement.

* Une nouvelle API est [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) créée pour récupérer les informations de profil pour un seul utilisateur. Il prend l’ID de l’équipe ou le chat et [un UPN](/windows/win32/ad/naming-properties#userprincipalname) qui `userPrincipalName` est , Azure Active Directory Object ID , ou `objectId` l’iD de l’utilisateur Teams `id` comme paramètres et renvoie les informations de profil pour cet utilisateur.

    > [!NOTE]
    > `objectId` est changé pour correspondre `aadObjectId` à ce qu’on appelle dans `Activity` l’objet d’un message Bot Framework. La nouvelle API est disponible avec la version 4.8 ou plus tard du Bot Framework SDK. Il est également disponible dans le Teams extension SDK Bot Framework 3.x. En attendant, vous pouvez utiliser le point de terminaison [REST.](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details)

* `TeamsInfo.GetMembersAsync` dans C# et `TeamsInfo.getMembers` dans TypeScript ou Node.js est formellement déprécié. Une fois que la nouvelle API est disponible, vous devez mettre à jour vos bots pour l’utiliser. Cela s’applique également à [l’API REST sous-jacente que ces API utilisent](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).
* À la fin de 2021, les bots ne peuvent pas récupérer de manière proactive les `userPrincipalName` propriétés ou les propriétés des membres `email` d’un chat ou d’une équipe. Les bots doivent utiliser Graph pour les récupérer. Les `userPrincipalName` propriétés et les propriétés ne sont pas `email` retournées de la nouvelle `GetConversationPagedMembers` API à partir de la fin de 2021. Les bots doivent utiliser Graph un jeton d’accès pour récupérer des informations. Il doit être plus facile pour les bots d’obtenir un jeton d’accès et de rationaliser et de simplifier le processus de consentement de l’utilisateur final.
