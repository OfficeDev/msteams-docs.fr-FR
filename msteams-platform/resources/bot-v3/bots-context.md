---
title: Obtenez le contexte pour votre bot Microsoft Teams
description: Décrit comment obtenir le contexte pour les bots dans Microsoft Teams
keywords: équipes bots contexte
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: cda2e24816330964342b097f52bb955c8846c54a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566487"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>Obtenez le contexte pour votre bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Votre bot peut accéder à un contexte supplémentaire sur l’équipe ou le chat, tel que le profil de l’utilisateur. Ces informations peuvent être utilisées pour enrichir les fonctionnalités de votre bot et fournir une expérience plus personnalisée.

> [!NOTE]
>
> * Microsoft Teams apis bot spécifiques sont mieux accessibles grâce à nos extensions pour le Bot Builder SDK.
> * Pour C# ou .NET, téléchargez [notre package Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.
> * Pour Node.js développement, le Bot Builder pour Teams fonctionnalité est incorporé dans [le Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.

## <a name="fetch-the-team-roster"></a>Aller chercher la liste de l’équipe

Votre bot peut demander la liste des membres de l’équipe et leurs profils de base. Les profils de base incluent Teams identifiants d’utilisateur et Azure Active Directory informations (AAD) telles que le nom et l’iD d’objet. Vous pouvez utiliser ces informations pour corréler l’identité des utilisateurs. Par exemple, vérifiez si un utilisateur connecté à un onglet via les informations d’identification AAD est un membre de l’équipe.

### <a name="rest-api-example"></a>EXEMPLE D’API REST

Émetez directement une demande GET sur [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) , en utilisant la valeur comme point `serviceUrl` final.

Le `teamId` peut être trouvé dans l’objet de la charge utile `channeldata` d’activité que votre bot reçoit dans les scénarios suivants:

* Lorsqu’un utilisateur messages ou interagit avec votre bot dans un contexte d’équipe. Pour plus d’informations, voir [recevoir des messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).
* Lorsqu’un nouvel utilisateur ou bot est ajouté à une équipe. Pour plus d’informations, voir [bot ou utilisateur ajouté à une équipe](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).

> [!NOTE]
>
>* Utilisez toujours l’iD de l’équipe lorsque vous appelez l’API.
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

Appelez `GetConversationMembersAsync` en utilisant pour retourner une liste `Team.Id` d’iD utilisateur.

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

### <a name="nodejs-or-typescript-example"></a>Node.js exemple de typeScript

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>Aller chercher le profil ou la liste de l’utilisateur dans le chat personnel ou de groupe

Vous pouvez faire appel à l’API pour n’importe quel chat personnel pour obtenir les informations de profil de l’utilisateur bavardant avec votre bot.

L’appel API, les méthodes SDK et l’objet de réponse sont identiques à la recherche de la liste d’équipe. La seule différence est que vous passez le `conversationId` lieu de la `teamId` .

## <a name="fetch-the-list-of-channels-in-a-team"></a>Aller chercher la liste des chaînes dans une équipe

Votre bot peut interroger la liste des canaux d’une équipe.

> [!NOTE]
>
>* Le nom du canal général par défaut est retourné `null` pour permettre la localisation.
>* L’ID de canal pour la chaîne Générale correspond toujours à l’ID de l’équipe.

### <a name="rest-api-example"></a>EXEMPLE D’API REST

Émetez directement une demande GET sur `/teams/{teamId}/conversations/` , en utilisant la valeur comme point `serviceUrl` final.

La seule source pour est `teamId` un message du contexte de l’équipe. Le message est soit un message d’un utilisateur, soit le message que votre bot reçoit lorsqu’il est ajouté à une équipe. Pour plus d’informations, voir [bot ou utilisateur ajouté à une équipe](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).

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

L’exemple suivant utilise `FetchChannelList` l’appel [des extensions Teams de la technologie pour le Bot Builder SDK pour .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js exemple

L’exemple suivant `fetchChannelList` utilise l’appel [Teams extensions de recherche pour le Bot Builder SDK pour Node.js](https://www.npmjs.com/package/botbuilder-teams):

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

## <a name="get-clientinfo-in-your-bot-context"></a>Obtenez clientInfo dans votre contexte bot

Vous pouvez aller chercher le clientInfo dans l’activité de votre bot. Le clientInfo contient les propriétés suivantes :

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

### <a name="c-example"></a>Exemple de C#

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a>Voir aussi

[Échantillons bot framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).