---
title: Modifications de l’API du bot pour les membres de l’équipe et de la conversation
author: ojasvichoudhary
description: Décrit les modifications à venir et en cours apportées aux API bot utilisées pour récupérer les membres des équipes et des conversations
keywords: liste des membres de l’équipe de l’infrastructure de bot
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: ee90c9c324f11e191cf596bcf8e27cd2bef41240
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596181"
---
# <a name="changes-to-teams-bot-apis-for-fetching-team-and-chat-members"></a>Modifications apportées aux API de bot Teams pour la récupération des membres d’équipe et de conversation

>[!NOTE]
> Nous avons commencé avec le processus de désintériation pour `TeamsInfo.getMembers` les `TeamsInfo.GetMembersAsync` API. Initialement, ils seront fortement limitées à 5 demandes par minute et retourneront un maximum de 10 000 membres par équipe. Ainsi, la liste complète n’est pas renvoyée à mesure que la taille de l’équipe augmente. 
> 
> Vous devez mettre à jour vers la **version 4.10** ou une version supérieure du SDK Bot Framework et basculer vers les points de terminaison de l’API paginée ou l’API utilisateur `TeamsInfo.GetMemberAsync` unique. Cela s’applique également à votre bot même si vous n’utilisez pas directement ces API, car les anciens SDK appellent ces API pendant les événements [MembersAdded.](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) Pour afficher la liste des modifications à venir, consultez [les modifications apportées aux API.](team-chat-member-api-changes.md#api-changes) 

Actuellement, les développeurs de bots qui souhaitent récupérer des informations pour un ou plusieurs membres d’une conversation ou d’une équipe utilisent les API de bot Microsoft Teams `TeamsInfo.GetMembersAsync` (pour C#) ou `TeamsInfo.getMembers` (pour TypeScript/Node.js) [(documentées ici).](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile) Ces API ont aujourd’hui plusieurs défauts :

* **Pour les grandes équipes, les performances sont médiocres et les délai d’exécution sont plus probables.** La taille maximale de l’équipe a considérablement augmenté depuis la publication de Microsoft Teams début 2017. Étant donné que renvoie l’intégralité de la liste des membres, le retour de l’appel d’API pour les grandes équipes prend beaucoup de temps, et il n’est pas rare que `GetMembersAsync` / l’appel n’approche pas du délai d’attente et que vous devez essayer à `getMembers` nouveau.
* **L’obtention des détails de profil pour un seul utilisateur est fastidieuse.** Pour obtenir les informations de profil d’un seul utilisateur, vous devez récupérer l’intégralité de la liste des membres, puis rechercher celle que vous souhaitez. Vrai, il existe une fonction d’aide dans le SDK Bot Framework pour le simplifier, mais en réalité, elle n’est pas efficace.

Séparément, avec l’introduction des équipes à l’échelle de l’organisation, nous avons compris qu’il était temps de mieux aligner ces API avec les contrôles de confidentialité Office 365 : les bots utilisés dans les grandes équipes peuvent récupérer des informations de profil de base, ce qui est similaire à l’autorisation `User.ReadBasic.All` Microsoft Graph. Les administrateurs clients contrôlent de manière très grande les applications et les bots qui peuvent être utilisés dans leur client, mais ces paramètres sont différents de ceux qui régissent Microsoft Graph.

Voici un exemple de représentation JSON de ce qui est renvoyé aujourd’hui par ces API. Je vais faire référence à certains des champs ci-dessous.

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

* Nous avons créé une API pour récupérer les informations de profil des membres [`TeamsInfo.GetPagedMembersAsync`](~/bots/how-to/get-teams-context.md?tabs=dotnet#fetching-the-roster-or-user-profile) d’une conversation/équipe. Cette API est désormais disponible avec le SDK Bot Framework 4.10. Pour le développement dans toutes les autres versions, utilisez la [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) méthode.
  > [!NOTE]
  > Dans la version v3 ou v4, la meilleure action consiste à mettre à niveau vers la dernière version de point.
* Nous avons créé une nouvelle API pour récupérer les informations de [`TeamsInfo.GetMemberAsync`](~/bots/how-to/get-teams-context.md?tabs=dotnet#get-single-member-details) profil d’un seul utilisateur. Il prend l’ID de l’équipe/la conversation et un [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) ( voir ci-dessus ), Azure Active Directory Object ID ( , voir ci-dessus ), ou l’ID utilisateur Teams ( , voir ci-dessus ) comme paramètres et renvoie les informations de profil pour cet `userPrincipalName`  `objectId`  `id` utilisateur. 
  > [!NOTE]
  > Nous changeons pour correspondre à ce `objectId` `aadObjectId` qu’il est appelé dans `Activity` l’objet d’un message Bot Framework. La nouvelle API est disponible avec la version 4.10 du SDK Bot Framework. Il sera bientôt disponible dans l’extension SDK Teams Bot Framework 3.x également . pendant ce temps, vous pouvez utiliser le point de terminaison [REST.](~/bots/how-to/get-teams-context.md?tabs=json#get-single-member-details)
* `TeamsInfo.GetMembersAsync` (C#) et (TypeScript/Node.js) sont officiellement supprimés et cesseront de fonctionner fin `TeamsInfo.getMembers` 2021. Mettez à jour vos bots pour utiliser les API pagiée. (Cela s’applique également à [l’API REST sous-jacente que ces API utilisent.)](~/bots/how-to/get-teams-context.md?tabs=json)
* Fin 2021, les bots ne pourront pas récupérer de manière proactive les propriétés des membres d’une conversation/équipe et devront utiliser Microsoft Graph pour `userPrincipalName` `email` les récupérer. Plus précisément, les propriétés ne seront pas renvoyées à partir de la nouvelle API à partir `userPrincipalName` `email` de la fin `GetConversationPagedMembers` 2021. Les bots devront utiliser Microsoft Graph avec un jeton d’accès pour récupérer ces informations. Il s’agit évidemment d’une modification majeure : nous devons faciliter l’accès des bots à un jeton d’accès, et rationaliser et simplifier le processus de consentement de l’utilisateur final.

## <a name="feedback-and-more-information"></a>Commentaires et plus d’informations

Nous utiliserons cette page pour fournir des informations à jour sur ces modifications. Si vous avez des questions, utilisez la section « Envoyer > commentaires sur cette page » dans la section **Commentaires ci-dessous.**
