---
title: Obtenir le contexte de votre bot Microsoft Teams de recherche
description: Décrit comment obtenir du contexte pour les bots dans Microsoft Teams
keywords: contexte des bots teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 5c9dac9712f6bdc9a62262614ceaf90fd100e19e
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155873"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Obtenir le contexte de votre bot Microsoft Teams de recherche

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Votre bot peut accéder à un contexte supplémentaire sur l’équipe ou la conversation, tel que le profil utilisateur. Ces informations peuvent être utilisées pour enrichir les fonctionnalités de votre bot et offrir une expérience plus personnalisée.

> [!NOTE]
>
> * Microsoft Teams’API de bot spécifiques sont les plus accessibles via nos extensions pour le SDK Bot Builder.
> * Pour C# ou .NET, téléchargez notre package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.
> * Pour Node.js développement, le Générateur de bot pour Teams est intégré au [SDK Bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.

## <a name="fetch-the-team-roster"></a>Récupérer la liste d’équipe

Votre bot peut interroger la liste des membres de l’équipe et leurs profils de base. Les profils de base incluent Teams’ID d’utilisateur et Azure Active Directory (AAD) tels que le nom et l’ID d’objet. Vous pouvez utiliser ces informations pour corréler les identités des utilisateurs. Par exemple, vérifiez si un utilisateur connecté à un onglet via les informations d’identification AAD est membre de l’équipe.

### <a name="rest-api-example"></a>Exemple d’API REST

Émettre directement une requête GET sur [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) , en utilisant la valeur comme point de `serviceUrl` terminaison.

Vous pouvez le trouver dans l’objet de la charge utile d’activité que votre `teamId` `channeldata` bot reçoit dans les scénarios suivants :

* Lorsqu’un utilisateur échange des messages ou interagit avec votre bot dans un contexte d’équipe. Pour plus d’informations, voir [la réception de messages.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)
* Lorsqu’un nouvel utilisateur ou bot est ajouté à une équipe. Pour plus d’informations, [voir bot ou utilisateur ajouté à une équipe.](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)

> [!NOTE]
>
>* Utilisez toujours l’ID d’équipe lors de l’appel de l’API.
>* La `serviceUrl` valeur tend à être stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur `serviceUrl` stockée.

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

Appel `GetConversationMembersAsync` utilisé `Team.Id` pour renvoyer une liste d’ID d’utilisateur.

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

### <a name="nodejs-or-typescript-example"></a>Node.js exemple ou TypeScript

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Récupérer le profil ou la liste d’utilisateurs dans une conversation personnelle ou de groupe

Vous pouvez appeler l’API pour toute conversation personnelle afin d’obtenir les informations de profil de l’utilisateur qui discute avec votre bot.

L’appel d’API, les méthodes du SDK et l’objet de réponse sont identiques à la récupération de la liste d’équipe. La seule différence est que vous passez le `conversationId` . `teamId`

## <a name="fetch-the-list-of-channels-in-a-team"></a>Récupérer la liste des canaux d’une équipe

Votre bot peut interroger la liste des canaux d’une équipe.

> [!NOTE]
>
>* Le nom du canal général par défaut est renvoyé pour `null` autoriser la localisation.
>* L’ID de canal pour le canal général correspond toujours à l’ID d’équipe.

### <a name="rest-api-example"></a>Exemple d’API REST

Émettre directement une requête GET sur `/teams/{teamId}/conversations/` , en utilisant la valeur comme point de `serviceUrl` terminaison.

La seule source est `teamId` un message du contexte d’équipe. Le message est un message d’un utilisateur ou le message que votre bot reçoit lorsqu’il est ajouté à une équipe. Pour plus d’informations, [voir bot ou utilisateur ajouté à une équipe.](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)

> [!NOTE]
> La `serviceUrl` valeur tend à être stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur `serviceUrl` stockée.

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

L’exemple suivant utilise l’appel des extensions Teams pour le `FetchChannelList` [SDK Bot Builder pour .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js exemple

L’exemple suivant utilise `fetchChannelList` l’appel des extensions Teams pour le [SDK Bot Builder pour Node.js](https://www.npmjs.com/package/botbuilder-teams):

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

## <a name="get-clientinfo-in-your-bot-context"></a>Obtenir clientInfo dans le contexte de votre bot

Vous pouvez extraire le clientInfo au sein de l’activité de votre bot. ClientInfo contient les propriétés suivantes :

* Locale
* Pays
* Plateforme
* Fuseau horaire

### <a name="json-example"></a>Exemple JSON

```json
[
    {
        "type": "clientInfo",
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "Asia/Calcutta"
    }
]
```

### <a name="c-example"></a>C# exemple

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)