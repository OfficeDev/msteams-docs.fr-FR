---
title: Obtenir le contexte de votre bot Microsoft Teams
description: Dans ce module, découvrez comment obtenir le contexte des bots dans Microsoft Teams, extraire la liste d’équipe et le profil utilisateur ou la liste de liste dans une conversation personnelle ou de groupe
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 3fd75e063f9b12c09bc4dded167bd8cdaead6b7a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143115"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Obtenir le contexte de votre bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Votre bot peut accéder à un contexte supplémentaire sur l’équipe ou la conversation, tel que le profil utilisateur. Ces informations peuvent être utilisées pour enrichir les fonctionnalités de votre bot et offrir une expérience plus personnalisée.

> [!NOTE]
>
> * Microsoft Teams API de bot spécifiques sont mieux accessibles via nos extensions pour le Kit de développement logiciel (SDK) Bot Builder.
> * Pour C# ou .NET, téléchargez notre package [de NuGet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).
> * Pour Node.js développement, la fonctionnalité Bot Builder pour Teams est incorporée dans le [Kit de développement logiciel (SDK) Bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.

## <a name="fetch-the-team-roster"></a>Récupérer la liste d’équipe

Votre bot peut rechercher la liste des membres de l’équipe et leurs profils de base. Les profils de base incluent des ID d’utilisateur Teams et des informations Microsoft Azure Active Directory (Azure AD), telles que le nom et l’ID d’objet. Vous pouvez utiliser ces informations pour mettre en corrélation les identités des utilisateurs. Par exemple, vérifiez si un utilisateur connecté à un onglet via des informations d’identification Microsoft Azure Active Directory (Azure AD) est un membre de l’équipe.

### <a name="rest-api-example"></a>Exemple d’API REST

Émettez directement une requête GET, [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)en utilisant la `serviceUrl` valeur comme point de terminaison.

Le `teamId` fichier se trouve dans l’objet `channeldata` de la charge utile d’activité que votre bot reçoit dans les scénarios suivants :

* Lorsqu’un utilisateur envoie des messages ou interagit avec votre bot dans un contexte d’équipe. Pour plus d’informations, consultez [réception de messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).
* Lorsqu’un nouvel utilisateur ou bot est ajouté à une équipe. Pour plus d’informations, consultez [bot ou utilisateur ajouté à une équipe](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).

> [!NOTE]
>
>* Utilisez toujours l’ID d’équipe lors de l’appel de l’API.
>* La `serviceUrl` valeur a tendance à être stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée `serviceUrl` .

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

Appeler `GetConversationMembersAsync` à l’aide `Team.Id` pour retourner une liste d’ID d’utilisateur.

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

### <a name="nodejs-or-typescript-example"></a>exemple Node.js ou TypeScript

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Récupérer un profil ou une liste d’utilisateurs dans une conversation personnelle ou de groupe

Vous pouvez effectuer l’appel d’API pour toute conversation personnelle afin d’obtenir les informations de profil de l’utilisateur qui discute avec votre bot.

L’appel d’API, les méthodes du Kit de développement logiciel (SDK) et l’objet de réponse sont identiques à l’extraction de la liste d’équipe. La seule différence est que vous passez la `conversationId` place de la `teamId`.

## <a name="fetch-the-list-of-channels-in-a-team"></a>Récupérer la liste des canaux dans une équipe

Votre bot peut interroger la liste des canaux d’une équipe.

> [!NOTE]
>
>* Le nom du canal Général par défaut est retourné en tant que `null` pour permettre la localisation.
>* L’ID de canal du canal Général correspond toujours à l’ID d’équipe.

### <a name="rest-api-example"></a>Exemple d’API REST

Émettez directement une requête GET, `/teams/{teamId}/conversations/`en utilisant la `serviceUrl` valeur comme point de terminaison.

La seule source est `teamId` un message du contexte d’équipe. Le message est soit un message d’un utilisateur, soit le message que votre bot reçoit lorsqu’il est ajouté à une équipe. Pour plus d’informations, consultez [bot ou utilisateur ajouté à une équipe](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).

> [!NOTE]
> La `serviceUrl` valeur a tendance à être stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée `serviceUrl` .

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

L’exemple suivant utilise l’appel `FetchChannelList` des [extensions Teams pour le Kit de développement logiciel (SDK) Bot Builder pour .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) :

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Exemple Node.js

L’exemple suivant utilise l’appel des [extensions Teams pour le Kit de développement logiciel (SDK) Bot Builder pour Node.js](https://www.npmjs.com/package/botbuilder-teams):`fetchChannelList`

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

Vous pouvez extraire le clientInfo dans l’activité de votre bot. ClientInfo contient les propriétés suivantes :

* Locale
* Pays
* Plateforme
* Timezone

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

### <a name="c-example"></a>Exemple C#

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
