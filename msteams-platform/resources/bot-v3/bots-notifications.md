---
title: Gérer les événements bot
description: Décrit comment gérer les événements dans les robots pour Microsoft teams
keywords: événements bots de teams
ms.date: 05/20/2019
ms.openlocfilehash: 06da5e6b0668e86012d87af3184493cdeb70aecd
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801078"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Gérer les événements bot dans Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft teams envoie des notifications à votre bot pour des modifications ou des événements qui se produisent dans les étendues où votre bot est actif. Vous pouvez utiliser ces événements pour déclencher la logique de service, par exemple :

* Déclencher un message de bienvenue lorsque votre bot est ajouté à une équipe
* Informations sur les groupes de requêtes et de cache lorsque le bot est ajouté à une conversation de groupe
* Mettre à jour les informations mises en cache sur l’appartenance ou les informations de canal de l’équipe
* Supprimer les informations mises en cache pour une équipe si le bot est supprimé
* Quand un message bot est aimé par un utilisateur

Chaque événement bot est envoyé sous la forme d’un `Activity` objet qui définit les informations contenues `messageType` dans l’objet. Pour les messages de type `message` , consultez la rubrique [envoi et réception de messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Les événements teams et Group, généralement déclenchés `conversationUpdate` par le type, ont des informations d’événements teams supplémentaires transmises dans le cadre de l' `channelData` objet et, par conséquent, votre gestionnaire d’événements doit interroger la `channelData` charge utile pour les équipes `eventType` et les métadonnées propres aux événements supplémentaires.

Le tableau suivant répertorie les événements que votre bot peut recevoir et comment agir.

|Type|Objet Payload|EventType teams |Description|Portée|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Membre ajouté à Team](#team-member-or-bot-addition)| tous les |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[Le membre a été supprimé de Team](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [L’équipe a été renommée](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Un canal a été créé](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Un canal a été renommé.](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Un canal a été supprimé](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Message de réaction au bot](#reactions)| tous les |
| `messageReaction` |`reactionsRemoved`|| [Réaction supprimée du message bot](#reactions)| tous les |

## <a name="team-member-or-bot-addition"></a>Ajout d’un membre d’équipe ou d’un bot

L' [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) événement est envoyé à votre bot lorsqu’il reçoit des informations sur les mises à jour d’appartenance de teams dans lesquelles il a été ajouté. Il reçoit également une mise à jour lorsqu’il a été ajouté pour la première fois, spécifiquement pour les conversations personnelles. Notez que les informations utilisateur ( `Id` ) sont uniques pour votre robot et peuvent être mises en cache pour une utilisation future par votre service (par exemple, l’envoi d’un message à un utilisateur spécifique).

### <a name="bot-or-user-added-to-a-team"></a>Bot ou utilisateur ajouté à une équipe

L' `conversationUpdate` événement dont l' `membersAdded` objet est dans la charge utile est envoyé lorsqu’un bot est ajouté à une équipe ou lorsqu’un nouvel utilisateur est ajouté à une équipe dans laquelle un bot a été ajouté. Microsoft teams ajoute également `eventType.teamMemberAdded` dans l' `channelData` objet.

Étant donné que cet événement est envoyé dans les deux cas, vous devez analyser l' `membersAdded` objet pour déterminer si l’ajout était un utilisateur ou le robot lui-même. Pour ce dernier, il est recommandé d’envoyer un [message de bienvenue](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) à la chaîne afin que les utilisateurs puissent comprendre les fonctionnalités fournies par votre robot.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Exemple de code : vérification du fait que bot était le membre ajouté

##### <a name="net"></a>.NET

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a>Node.js

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a>Exemple de schéma : Bot ajouté à Team

```json
{
    "membersAdded": [
        {
            "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:38:35.312Z",
    "localTimestamp": "2017-02-23T12:38:35.312-07:00",
    "id": "f:5f85c2ad",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="bot-added-for-personal-context-only"></a>Bot ajouté uniquement pour le contexte personnel

Votre bot reçoit un `conversationUpdate` avec `membersAdded` lorsqu’un utilisateur l’ajoute directement pour la conversation personnelle. Dans ce cas, la charge utile que reçoit votre bot ne contient pas l' `channelData.team` objet. Vous devez l’utiliser comme filtre si vous souhaitez que votre bot propose un autre message d' [Accueil](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) en fonction de l’étendue.

> [!NOTE]
> Pour les robots personnels, votre robot ne recevra jamais l' `conversationUpdate` événement qu’une seule fois, même si le bot est supprimé et rajouté. Pour le développement et les tests, il peut s’avérer utile d’ajouter une fonction d’assistance qui vous permettra de réinitialiser entièrement votre robot. Pour plus d’informations sur l’implémentation de cet exemple, voir un exemple de [Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) ou [C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) .

#### <a name="schema-example-bot-added-to-personal-context"></a>Exemple de schéma : Bot ajouté au contexte personnel

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

## <a name="team-member-or-bot-removed"></a>Membre d’équipe supprimé

L' `conversationUpdate` événement dont l' `membersRemoved` objet est dans la charge utile est envoyé lorsque le robot est supprimé d’une équipe ou lorsqu’un utilisateur est supprimé d’une équipe dans laquelle un bot a été ajouté. Microsoft teams ajoute également `eventType.teamMemberRemoved` dans l' `channelData` objet. Comme avec l' `membersAdded` objet, vous devez analyser l' `membersRemoved` objet pour identifier l’ID de l’application de votre bot afin de déterminer qui a été supprimé.

### <a name="schema-example-team-member-removed"></a>Exemple de schéma : membre d’équipe supprimé

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="team-name-updates"></a>Mises à jour de nom d’équipe

> [!NOTE]
> Il n’existe aucune fonctionnalité permettant d’interroger tous les noms d’équipe et le nom de l’équipe n’est pas renvoyé dans les charges par d’autres événements.

Votre robot est informé de la modification du nom de l’équipe dans laquelle il se trouve. Elle reçoit un `conversationUpdate` événement avec `eventType.teamRenamed` dans l' `channelData` objet. Veuillez noter qu’il n’existe aucune notification pour la création ou la suppression d’une équipe, car les robots n’existent que dans le cadre de teams et n’ont aucune visibilité en dehors de l’étendue dans laquelle ils ont été ajoutés.

### <a name="schema-example-team-renamed"></a>Exemple de schéma : équipe renommée

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="channel-updates"></a>Mises à jour de canal

Votre robot est averti lorsqu’un canal est créé, renommé ou supprimé dans une équipe où il a été ajouté. Une fois encore, l' `conversationUpdate` événement est reçu et un identificateur d’événement spécifique à teams est envoyé dans le cadre de l' `channelData.eventType` objet, où les données du canal `channel.id` sont le GUID du canal et `channel.name` contient le nom du canal lui-même.

Les événements de canal sont les suivants :

* **channelCreated** &emsp; Un utilisateur ajoute un nouveau canal à l’équipe
* **channelRenamed** &emsp; Un utilisateur renomme un canal existant
* **channelDeleted** &emsp; Un utilisateur supprime un canal

### <a name="full-schema-example-channelcreated"></a>Exemple de schéma complet : channelCreated

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Extrait de schéma : channelData pour channelRenamed

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelRenamed",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>Extrait de schéma : channelData pour channelDeleted

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelDeleted",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

## <a name="reactions"></a>Réactions

L' `messageReaction` événement est envoyé lorsqu’un utilisateur ajoute ou supprime sa réaction à un message qui a été envoyé par votre bot. `replyToId`contient l’ID du message spécifique.

### <a name="schema-example-a-user-likes-a-message"></a>Exemple de schéma : un utilisateur aime un message

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a>Exemple de schéma : un utilisateur n’aime pas un message

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```
