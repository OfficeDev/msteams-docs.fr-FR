---
title: Gérer les événements bot
description: Décrit comment gérer les événements dans les bots pour Microsoft Teams
keywords: équipes bots événements
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: da624ea0e92e193f4ad7f334d958349d542dd6e0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566466"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>Gérer les événements bot dans Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams envoie des notifications à votre bot pour les modifications ou les événements qui se produisent dans les étendues où votre bot est actif. Vous pouvez utiliser ces événements pour déclencher la logique de service, telles que les éléments suivants :

* Déclenchez un message de bienvenue lorsque votre bot est ajouté à une équipe.
* Requête et cache d’informations de groupe lorsque le bot est ajouté à un chat de groupe.
* Mettre à jour les informations mises en cache sur l’adhésion à l’équipe ou les informations de canal.
* Supprimez les informations mises en cache pour une équipe si le bot est supprimé.
* Lorsqu’un message bot est aimé par un utilisateur.

Chaque événement bot est envoyé comme un `Activity` objet dans lequel définit quelles informations sont dans `messageType` l’objet. Pour les messages de type `message` , voir Envoi et réception de [messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).

Teams et les événements de groupe, généralement déclenchés hors `conversationUpdate` du type, ont des informations d’événement Teams supplémentaires transmises dans le cadre `channelData` de l’objet, et donc votre gestionnaire d’événements doit interroger la `channelData` charge utile pour les Teams et les `eventType` métadonnées supplémentaires spécifiques à l’événement.

Le tableau suivant énumère les événements que votre bot peut recevoir et prendre des mesures.

|Type|Objet de charge utile|Teams événementType |Description|Portée|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[Membre ajouté à l’équipe](#team-member-or-bot-addition)| tout |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[Membre a été retiré de l’équipe](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [L’équipe a été rebaptisée](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [Un canal a été créé](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [Une chaîne a été rebaptisée](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [Un canal a été supprimé](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [Réaction au message bot](#reactions)| tout |
| `messageReaction` |`reactionsRemoved`|| [Réaction supprimée du message bot](#reactions)| tout |

## <a name="team-member-or-bot-addition"></a>Membre de l’équipe ou ajout de bot

[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true)L’événement est envoyé à votre bot lorsqu’il reçoit des informations sur les mises à jour des membres pour les équipes où il a été ajouté. Il reçoit également une mise à jour lorsqu’il a été ajouté pour la première fois, spécifiquement pour les conversations personnelles. Notez que les informations utilisateur ( `Id` ) est unique pour votre bot et peut être mis en cache pour une utilisation future par votre service, comme, l’envoi d’un message à un utilisateur spécifique.

### <a name="bot-or-user-added-to-a-team"></a>Bot ou utilisateur ajouté à une équipe

`conversationUpdate`L’événement avec `membersAdded` l’objet dans la charge utile est envoyé lorsqu’un bot est ajouté à une équipe ou qu’un nouvel utilisateur est ajouté à une équipe où un bot a été ajouté. Microsoft Teams ajoute également `eventType.teamMemberAdded` dans `channelData` l’objet.

Étant donné que cet événement est envoyé dans les deux cas, vous devez examiner `membersAdded` l’objet pour déterminer si l’ajout était un utilisateur ou le bot lui-même. Pour ce dernier, une bonne pratique est d’envoyer un [message de bienvenue au](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) canal afin que les utilisateurs puissent comprendre les fonctionnalités de votre bot fournit.

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>Exemple de code : Vérifier si bot était le membre ajouté

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

#### <a name="schema-example-bot-added-to-team"></a>Exemple de schéma : Bot ajouté à l’équipe

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a>Utilisateur ajouté à une réunion

`conversationUpdate`L’événement avec `membersAdded` l’objet dans la charge utile est envoyé lorsqu’un utilisateur est ajouté à une réunion privée planifiée. Les détails de l’événement seront envoyés même lorsque des utilisateurs anonymes se joindront à la réunion. 

> [!NOTE]
>
>* Lorsqu’un utilisateur anonyme est ajouté à une réunion, l’objet de charge utile membersAdded n’a pas de `aadObjectId` champ.
>* Lorsqu’un utilisateur anonyme est ajouté à une réunion, `from` l’objet de la charge utile a toujours l’id de l’organisateur de la réunion, même si l’utilisateur anonyme a été ajouté par un autre présentateur.

#### <a name="schema-example-user-added-to-meeting"></a>Exemple de schéma : Utilisateur ajouté à la réunion

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a>Bot ajouté pour le contexte personnel seulement

Votre bot reçoit un `conversationUpdate` avec quand un utilisateur `membersAdded` l’ajoute directement pour le chat personnel. Dans ce cas, la charge utile que votre bot reçoit ne contient pas `channelData.team` l’objet. Vous devez l’utiliser comme filtre au cas où vous souhaitez que votre bot offre un message de [bienvenue différent en fonction](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) de la portée.

> [!NOTE]
> Pour les bots personnels, votre bot recevra `conversationUpdate` l’événement plusieurs fois, même si le bot est supprimé et ré-ajouté. Pour le développement et les tests, vous trouverez peut-être utile d’ajouter une fonction d’aide qui vous permettra de réinitialiser complètement votre bot. Voir un exemple [Node.js C# pour](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) [plus de détails sur la](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) mise en œuvre de cette.

#### <a name="schema-example-bot-added-to-personal-context"></a>Exemple de schéma : bot ajouté au contexte personnel

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

## <a name="team-member-or-bot-removed"></a>Membre de l’équipe ou bot retiré

`conversationUpdate`L’événement avec `membersRemoved` l’objet dans la charge utile est envoyé lorsque votre bot est retiré d’une équipe, ou qu’un utilisateur est retiré d’une équipe où un bot a été ajouté. Microsoft Teams ajoute également `eventType.teamMemberRemoved` dans `channelData` l’objet. Comme pour `membersAdded` l’objet, vous devez parse `membersRemoved` l’objet de l’ID app de votre bot pour déterminer qui a été supprimé.

### <a name="schema-example-team-member-removed"></a>Exemple de schéma : Membre de l’équipe supprimé

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

### <a name="user-removed-from-a-meeting"></a>Utilisateur retiré d’une réunion

`conversationUpdate`L’événement avec `membersRemoved` l’objet dans la charge utile est envoyé lorsqu’un utilisateur est retiré d’une réunion planifiée privée. Les détails de l’événement seront envoyés même lorsque des utilisateurs anonymes se joindront à la réunion. 

> [!NOTE]
>
>* Lorsqu’un utilisateur anonyme est retiré d’une réunion, l’objet de charge utile de membersRemoved n’a pas `aadObjectId` de champ.
>* Lorsqu’un utilisateur anonyme est retiré d’une réunion, `from` l’objet de la charge utile a toujours l’id de l’organisateur de la réunion, même si l’utilisateur anonyme a été supprimé par un autre présentateur.

#### <a name="schema-example-user-removed-from-meeting"></a>Exemple de schéma : Utilisateur retiré de la réunion

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a>Mises à jour des noms d’équipe

> [!NOTE]
> Il n’y a aucune fonctionnalité pour interroger tous les noms d’équipe, et le nom de l’équipe n’est pas retourné dans les charges utiles d’autres événements.

Votre bot est notifié lorsque l’équipe dans qui il se trouve a été rebaptisée. Il reçoit un `conversationUpdate` événement avec dans `eventType.teamRenamed` `channelData` l’objet. Veuillez noter qu’il n’y a pas de notifications pour la création ou la suppression d’équipes, car les bots n’existent que dans le cadre d’équipes et n’ont aucune visibilité en dehors du champ d’application dans lequel ils ont été ajoutés.

### <a name="schema-example-team-renamed"></a>Exemple de schéma : Équipe renommée

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

## <a name="channel-updates"></a>Mises à jour des canaux

Votre bot est notifié lorsqu’un canal est créé, renommé ou supprimé dans une équipe où il a été ajouté. Encore une fois, `conversationUpdate` l’événement est reçu, et un identificateur d’événement spécifique à Teams est envoyé dans le cadre de `channelData.eventType` l’objet, où les données du canal est le GUID pour le `channel.id` canal, et `channel.name` contient le nom du canal lui-même.

Les événements de la chaîne sont les suivants:

* **canalCréé** &emsp; Un utilisateur ajoute un nouveau canal à l’équipe.
* **canalRenamed** &emsp; Un utilisateur renomme un canal existant.
* **canalDeleted** &emsp; Un utilisateur supprime un canal.

### <a name="full-schema-example-channelcreated"></a>Exemple complet de schéma : canalCréé

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>Extrait de Schema: channelData pour channelRenamed

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>Extrait de Schema: channelData pour channelDeleted

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

`messageReaction`L’événement est envoyé lorsqu’un utilisateur ajoute ou supprime sa réaction à un message qui a été envoyé à l’origine par votre bot. `replyToId` contient l’ID du message spécifique.

### <a name="schema-example-a-user-likes-a-message"></a>Exemple de schéma : Un utilisateur aime un message

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

### <a name="schema-example-a-user-un-likes-a-message"></a>Exemple de schéma : un utilisateur n’aime pas un message

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
