---
title: Modifications de l’API bot pour les membres Team/Chat (mise à jour 2020)
author: ojasvichoudhary
description: Décrit les modifications à venir et en cours pour les API bot utilisées pour extraire des membres de teams et des conversations
keywords: Liste des membres de l’équipe des API de l’infrastructure bot
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 926e4e39e4b5c3f1ba34a4458cf6f17612d86841
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/28/2020
ms.locfileid: "44801102"
---
# <a name="changes-to-teams-bot-apis-for-fetching-teamchat-members"></a>Modifications apportées aux API de robots teams pour la récupération des membres de l’équipe/conversation

Actuellement, les développeurs de robots qui souhaitent récupérer des informations pour un ou plusieurs membres d’une conversation ou d’une équipe utilisent les API Microsoft teams bot `TeamsInfo.GetMembersAsync` (pour C#) ou `TeamsInfo.getMembers` (pour la machine à écrire/Node.js) [(documentée ici)](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile). Ces API présentent aujourd’hui plusieurs lacunes :

* **Pour les grandes équipes, les performances sont médiocres et les délais d’attente sont plus probables.** La taille maximale de l’équipe a augmenté considérablement depuis la publication de Microsoft teams en début de 2017. Étant donné que `GetMembersAsync` / `getMembers` renvoie la liste des membres dans son intégralité, l’appel de l’API prend beaucoup de temps pour être renvoyé pour les grandes équipes et n’est pas rare pour l’appel au délai d’expiration et vous devez recommencer.
* **L’obtention des détails du profil pour un seul utilisateur est lourde.** Pour obtenir les informations de profil d’un utilisateur, vous devez récupérer toute la liste de membres, puis Rechercher celle de votre choix. True, il y a une fonction d’assistance dans le kit de développement logiciel (SDK) de l’infrastructure pour faciliter sa création, mais sous les couvertures, elle n’est pas efficace.

Séparément, avec l’introduction de teams à l’échelle de l’organisation, nous avons réalisé qu’il était temps de mieux aligner ces API avec les contrôles de confidentialité Office 365 : les robots utilisés dans les grandes équipes sont en mesure de récupérer des informations de profil de base, qui sont semblables à l' `User.ReadBasic.All` autorisation Microsoft Graph. Les administrateurs clients ont beaucoup de contrôle sur les applications et les robots pouvant être utilisés dans leur client, mais ces paramètres diffèrent de ceux qui régissent Microsoft Graph.

Voici un exemple de représentation JSON de ce qui est renvoyé par ces API dès aujourd’hui. Voici quelques-uns des champs ci-dessous.

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com"
}]
```

## <a name="api-changes"></a>Modifications de l’API
Voici les modifications d’API à venir :

* Nous avons créé une nouvelle API [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile) pour récupérer des informations de profil pour les membres d’une conversation/équipe. Cette API est désormais disponible avec le kit de développement logiciel (SDK) de robot Framework 4,8. Pour le développement dans toutes les autres versions, utilisez la [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable) méthode. **Remarque**: dans la version 3 ou v4, la meilleure mesure consiste à effectuer une mise à niveau vers la version la plus récente (3.30.2 ou 4,8, respectivement). 
* Nous avons créé une nouvelle API [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) pour extraire les informations de profil pour un utilisateur unique. Il prend l’ID de l’équipe/conversation et un [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) ( `userPrincipalName` , *voir ci-dessus*), Azure Active Directory Object ID ( `objectId` , *voir ci-dessus*) ou l’ID utilisateur Teams ( `id` *voir ci-dessus*) comme paramètres et renvoie les informations de profil de cet utilisateur. **Remarque**: nous modifions `objectId` pour qu' `aadObjectId` il corresponde à ce qu’il est appelé dans l' `Activity` objet d’un message de l’infrastructure bot. La nouvelle API est disponible avec la version 4,8 du kit de développement logiciel (SDK) de l’infrastructure bot. Il sera bientôt disponible dans l’infrastructure de l’extension du kit de développement logiciel (SDK) teams 3. x. en attendant, vous pouvez utiliser le point de terminaison [Rest](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) .
* `TeamsInfo.GetMembersAsync`(C#) et `TeamsInfo.getMembers` (machine à écrire/Node.js) est explicitement déconseillée et cessera de fonctionner en fin de 2021. Nous annoncerons un calendrier spécifique en mai 2020 en fonction des commentaires des développeurs. Une fois la nouvelle API paginée disponible, les développeurs doivent mettre à jour leurs robots pour l’utiliser. (Ceci s’applique également à l' [API REST sous-jacente utilisée par ces API](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json).)
* En fin de 2021, les robots ne pourront pas récupérer de façon proactive les `userPrincipalName` `email` Propriétés ou pour les membres d’une équipe de conversation et devront utiliser Microsoft Graph pour les récupérer. Plus précisément `userPrincipalName` , `email` les propriétés ne seront pas renvoyées à partir de la nouvelle API à partir du `GetConversationPagedMembers` 2021. Les robots doivent utiliser Microsoft Graph avec un jeton d’accès pour récupérer ces informations. Il s’agit évidemment d’une modification majeure : nous devons permettre aux robots d’obtenir un jeton d’accès plus facilement, et nous devons rationaliser et simplifier le processus de consentement de l’utilisateur final.

## <a name="feedback-and-more-information"></a>Commentaires et informations supplémentaires
Nous allons utiliser cette page pour fournir des informations à jour sur ces modifications. Si vous avez des questions, utilisez le commentaire « envoyer des commentaires > sur cette page » dans la section **Commentaires** ci-dessous. 
