---
title: Obtenir le contexte de votre robot
description: Décrit comment obtenir le contexte des robots dans Microsoft teams
keywords: contexte des robots teams
ms.date: 05/20/2019
ms.openlocfilehash: 2dea6fd51e7274fa899d9ae882441a21618d7e09
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674024"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Obtenir le contexte de votre robot Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Votre robot peut accéder à un contexte supplémentaire concernant l’équipe ou la conversation, comme le profil utilisateur. Ces informations peuvent être utilisées pour enrichir les fonctionnalités de votre robot et fournir une expérience plus personnalisée.

> [!NOTE]
> Ces API de&ndash;robot spécifiques de Microsoft teams sont les meilleurs accessibles via nos extensions pour le kit de développement logiciel (SDK) du générateur de robots. Pour C#/.NET, téléchargez notre package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) . Pour le développement de node. js, vous pouvez installer le package NPM [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) . Les deux SDK Target Builder v3.

## <a name="fetching-the-team-roster"></a>Extraction de la liste de l’équipe

Votre robot peut demander la liste des membres de l’équipe et leurs profils de base, qui incluent les ID utilisateur teams et les informations Azure Active Directory (Azure AD), telles que nom et objectId. Vous pouvez utiliser ces informations pour corréler les identités des utilisateurs ; par exemple, pour vérifier si un utilisateur connecté à un onglet par le biais d’informations d’identification Azure AD est membre de l’équipe.

### <a name="rest-api-example"></a>Exemple d’API REST

Vous pouvez directement émettre une requête GET sur [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), en utilisant la valeur `serviceUrl` de comme point de terminaison.

Le `teamId` peut être trouvé dans l' `channeldata` objet de la charge utile d’activité que votre robot reçoit dans les scénarios suivants :
* Quand un utilisateur entre ou interagit avec votre robot dans un contexte d’équipe (voir [réception de messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))
* Lorsqu’un nouvel utilisateur ou robot est ajouté à une équipe (voir [bot ou User ajouté à une équipe](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))

> [!NOTE]
>* Veillez à utiliser l’ID d’équipe lors de l’appel de l’API.
>* La valeur de `serviceUrl` tend à être stable mais peut varier. Lors de l’arrivée d’un nouveau message, votre robot doit vérifier sa `serviceUrl`valeur stockée.

```json
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members

Response body
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

### <a name="net-example"></a>Exemple .NET

Appelez `GetConversationMembersAsync` using `Team.Id` pour renvoyer la liste des ID d’utilisateur.

```csharp
// Fetch the members in the current conversation
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));
var teamId = context.Activity.GetChannelData<TeamsChannelData>().Team.Id;
var members = await connector.Conversations.GetConversationMembersAsync(teamId);

// Concatenate information about all members into a string
var sb = new StringBuilder();
foreach (var member in members.AsTeamsChannelAccounts())
{
    sb.AppendFormat(
        "GivenName = {0}, TeamsMemberId = {1}",
        member.Name, member.Id);

    sb.AppendLine();
}

// Post the member info back into the conversation
await context.PostAsync($"People in this conversation: {sb.ToString()}");
```

### <a name="nodejstypescript-example"></a>Exemple node. js/machine à écrire

L’exemple suivant utilise les [extensions Microsoft teams pour le kit de développement logiciel (SDK) du générateur de robots pour node. js](https://www.npmjs.com/package/botbuilder-teams).

```typescript

[...]
import * as builder from "botbuilder";
[...]

var teamId = session.message.sourceEvent.team.id;
connector.fetchMembers(
  (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is some error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a>Extraction d’un profil utilisateur ou d’une liste dans la conversation personnelle ou de groupe

Vous pouvez également effectuer la même appel d’API pour toute conversation personnelle afin d’obtenir les informations de profil de l’utilisateur en conversation avec votre robot.

Les méthodes de l’appel de l’API et du kit de développement logiciel sont identiques à la récupération de la liste de l’équipe, comme l’est l’objet de réponse. La seule différence est que vous transmettez la `conversationId` à `teamId`la place de.

## <a name="fetching-the-list-of-channels-in-a-team"></a>Extraction de la liste des canaux dans une équipe

Votre robot peut interroger la liste des canaux d’une équipe.

> [!NOTE]
>
>* Le nom du canal général par défaut est renvoyé en `null` tant que pour permettre la localisation.
>* L’ID de canal pour le canal général correspond toujours à l’ID d’équipe.

### <a name="rest-api-example"></a>Exemple d’API REST

Vous pouvez directement émettre une requête GET sur `/teams/{teamId}/conversations/`, en utilisant la valeur `serviceUrl` de comme point de terminaison.

La seule source pour `teamId` est un message provenant du contexte de l’équipe, c’est-à-dire un message provenant d’un utilisateur ou d’un message que votre bot reçoit lorsqu’il est ajouté à une équipe (voir [bot ou User ajouté à une équipe](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).

> [!NOTE]
> La valeur de `serviceUrl` tend à être stable mais peut varier. Lors de l’arrivée d’un nouveau message, votre robot doit vérifier sa `serviceUrl`valeur stockée.

```json
GET /v3/teams/19%3A033451497ea84fcc83d17ed7fb08a1b6%40thread.skype/conversations

Response body
{
    "conversations": [{
        "id": "19:033451497ea84fcc83d17ed7fb08a1b6@thread.skype",
        "name": null
    }, {
        "id": "19:cc25e4aae50746ecbb11473bba24c70a@thread.skype",
        "name": "Materials"
    }, {
        "id": "19:b7b84cba410c406ba671dbbf5e0a3519@thread.skype",
        "name": "Design"
    }, {
        "id": "19:fc5db2aed489454e8f8c06829ed6c986@thread.skype",
        "name": "Marketing"
    }]
}
```

#### <a name="net-example"></a>Exemple .NET

L’exemple suivant utilise l' `FetchChannelList` appel de la part des [extensions de Microsoft teams pour le kit de développement logiciel (SDK) du générateur de robots pour .net](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Exemple node. js

L’exemple suivant utilise `fetchChannelList` Call à partir des [extensions Microsoft teams pour le kit de développement logiciel (SDK) du générateur de robots pour node. js](https://www.npmjs.com/package/botbuilder-teams).

```javascript
var teamId = session.message.sourceEvent.team.id;
connector.fetchChannelList(
  (session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is an error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```
