---
title: Événements de conversation
author: WashingtonKayaker
description: Utilisez les événements de conversation de votre bot Microsoft Teams, les mises à jour des événements de canal, les événements membres de l’équipe et les événements de réaction de message avec des exemples (.NET, Node.js,Python).
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: conversation de réaction au message du canal du bot d’événements
ms.openlocfilehash: 6bf1be094afc778317f2e4d5a7657514d35b9777
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100356"
---
# <a name="conversation-events-in-your-teams-bot"></a>Événements de conversation dans votre robot Teams

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Lorsque vous créez vos bots conversationnels pour Microsoft Teams, vous pouvez utiliser des événements de conversation. Teams envoie des notifications à votre bot pour les événements de conversation qui se produisent dans les étendues où votre bot est actif. Vous pouvez capturer ces événements dans votre code et effectuer les actions suivantes :

* Déclenchez un message de bienvenue lorsque votre bot est ajouté à une équipe.
* Déclenchez un message de bienvenue lorsqu’un nouveau membre d’équipe est ajouté ou supprimé.
* Déclenchez une notification lorsqu’un canal est créé, renommé ou supprimé.
* Déclenchez une notification lorsqu’un message de bot est aimé par un utilisateur.
* Identifiez le canal par défaut de votre bot à partir de l’entrée utilisateur (sélection) pendant l’installation.

## <a name="conversation-update-events"></a>Événements de mise à jour de conversation

Vous pouvez utiliser des événements de mise à jour de conversation pour fournir de meilleures notifications et des actions de bot efficaces.

> [!IMPORTANT]
>
> * Vous pouvez ajouter de nouveaux événements à tout moment et votre bot commence à les recevoir.
> * Vous devez concevoir votre bot pour recevoir des événements inattendus.
> * Si vous utilisez le SDK Bot Framework, votre bot répond automatiquement avec un `200 - OK` à tous les événements que vous choisissez de ne pas gérer.

Un bot reçoit un événement `conversationUpdate` dans l’un des cas suivants :

* Lorsque le bot a été ajouté à une conversation.
* D’autres membres sont ajoutés ou supprimés d’une conversation.
* Les métadonnées de conversation ont changé.

L’événement `conversationUpdate` est envoyé à votre robot lorsqu’il reçoit des informations sur les mises à jour d’appartenance pour les équipes dans lesquelles il a été ajouté. Il reçoit également une mise à jour lorsqu’elle a été ajoutée pour la première fois pour les conversations personnelles.

Le tableau suivant affiche une liste des événements de mise à jour de conversation Teams avec plus de détails :

| Action exécutée        | EventType         | Méthode appelée              | Description                | Portée |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| Chaîne créée     | channelCreated    | OnTeamsChannelCreatedAsync | [Un canal est créé](#channel-created). | Équipe |
| Canal renommé     | channelRenamed    | OnTeamsChannelRenamedAsync | [Un canal est renommé](#channel-renamed). | Équipe |
| Canal supprimé     | ChannelDeleted    | OnTeamsChannelDeletedAsync | [Un canal est supprimé](#channel-deleted). | Équipe |
| Canal restauré    | channelRestored    | OnTeamsChannelRestoredAsync | [Un canal est restauré](#channel-deleted). | Équipe |
| Membres ajoutés   | membersAdded   | OnTeamsMembersAddedAsync   | [Un membre est ajouté](#members-added). | Tous |
| Membres supprimés | membersRemoved | OnTeamsMembersRemovedAsync | [Un membre est supprimé](#members-removed). | Tous |
| Équipe renommée        | teamRenamed       | OnTeamsTeamRenamedAsync    | [Une équipe est renommée](#team-renamed).       | Équipe |
| Équipe supprimée        | TeamDeleted       | OnTeamsTeamDeletedAsync    | [Une équipe est supprimée](#team-deleted).       | Équipe |
| Équipe archivée        | teamArchived       | OnTeamsTeamArchivedAsync    | [Une équipe est archivée](#team-archived).       | Équipe |
| Équipe non archivée        | teamUnarchived       | OnTeamsTeamUnarchivedAsync    | [Une équipe n’est pasarchived](#team-unarchived).       | Équipe |
| Équipe restaurée        | teamRestored      | OnTeamsTeamRestoredAsync    | [Une équipe est restaurée](#team-restored)       | Équipe |

### <a name="channel-created"></a>Chaîne créée

L’événement `channelCreated` est envoyé à votre bot chaque fois qu’un nouveau canal est créé dans une équipe où votre bot est installé.

Le code suivant montre un exemple d’événement créé par un canal :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelCreatedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Created', `${channelInfo.name} is the Channel created`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_created(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(
   f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
  )
 )
```

---

### <a name="channel-renamed"></a>Canal renommé

L’événement `channelRenamed` est envoyé à votre bot chaque fois qu’un canal est renommé dans une équipe où votre bot est installé.

Le code suivant montre un exemple d’événement renommé de canal :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRenamedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Renamed', `${channelInfo.name} is the new Channel name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
```

# <a name="json"></a>[JSON](#tab/json)

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
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_renamed(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The new channel name is {channel_info.name}")
 )
```

---

### <a name="channel-deleted"></a>Canal supprimé

L’événement `channelDeleted` est envoyé à votre bot chaque fois qu’un canal est supprimé dans une équipe où votre bot est installé.

Le code suivant montre un exemple d’événement de suppression de canal :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelDeletedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Deleted', `${channelInfo.name} is the Channel deleted`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

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
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_deleted(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The deleted channel is {channel_info.name}")
 )
```

---

### <a name="channel-restored"></a>Canal restauré

L’événement `channelRestored` est envoyé à votre bot chaque fois qu’un canal précédemment supprimé est restauré dans une équipe où votre bot est déjà installé.

Le code suivant montre un exemple d’événement de restauration de canal :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRestoredEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Restored', `${channelInfo.name} is the Channel restored`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

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
        "eventType": "channelRestored",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_channel_restored(
 self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(
   f"The restored channel is {channel_info.name}. The channel id is {channel_info.id}"
  )
 )
```

---

### <a name="members-added"></a>Membres ajoutés

Un événement ajouté à un membre est envoyé à votre bot dans les scénarios suivants :

1. Lorsque le bot, lui-même, est installé et ajouté à une conversation

   > Dans le contexte de l’équipe, le conversation.id de l’activité est défini sur le `id` canal sélectionné par l’utilisateur pendant l’installation de l’application ou le canal sur lequel le bot a été installé.

2. Lorsqu’un utilisateur est ajouté à une conversation où le bot est installé

   > Les ID d’utilisateur reçus dans la charge utile de l’événement sont propres au bot et peuvent être mis en cache pour une utilisation ultérieure, comme la messagerie directe d’un utilisateur.

L’activité `eventType` ajoutée par le membre est définie sur `teamMemberAdded` le moment où l’événement est envoyé à partir d’un contexte d’équipe. Pour déterminer si le nouveau membre ajouté était le bot lui-même ou un utilisateur, vérifiez l’objet `Activity` du `turnContext`. Si la `MembersAdded` liste contient un objet où `id` est le même que le `id` champ de l’objet `Recipient` , le membre ajouté est le bot, sinon il s’agit d’un utilisateur. Le bot `id` est mis en forme en tant que `28:<MicrosoftAppId>`.

> [!TIP]
> Utilisez [l’événement`InstallationUpdate`](#installation-update-event) pour déterminer quand votre bot est ajouté ou supprimé d’une conversation.

Le code suivant montre un exemple d’événement ajouté par les membres de l’équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded , TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in teamsMembersAdded)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // Send a message to introduce the bot to the team
            var heroCard = new HeroCard(text: $"The {member.Name} bot has joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersAddedEvent(async (membersAdded: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
                let newMembers: string = '';
                console.log(JSON.stringify(membersAdded));
                membersAdded.forEach((account) => {
                    newMembers += account.id + ' ';
                });
                const name = !teamInfo ? 'not in team' : teamInfo.name;
                const card = CardFactory.heroCard('Account Added', `${newMembers} joined ${name}.`);
                const message = MessageFactory.attachment(card);
                await turnContext.sendActivity(message);
                await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

Message que votre bot reçoit lorsque celui-ci est ajouté à une équipe.

> [!NOTE]
> Dans cette charge utile, `conversation.id` il `channelData.settings.selectedChannel.id` s’agit de l’ID du canal sélectionné par l’utilisateur lors de l’installation de l’application ou de l’emplacement à partir duquel l’installation a été déclenchée.

```json
{
    "type": "conversationUpdate",
    "membersAdded": [
        {
            "id": "28:608cacfd-1cea-40c9-b678-4b93e69bb72b"
        }
    ],
    "timestamp": "2021-12-07T22:34:56.534Z",
    "id": "f:0b9079f4-d4d3-3d8e-b883-798298053c7e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1ljv6N86roXr5pjPrCJVIz6xHh5QxjI....",
        "aadObjectId": "eddfa9d4-346e-4cce-a18f-fa6261ad776b"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "tenantId": "b28fdbfd-2b78-4f93-b0f8-8881793f0f8f",
        "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2",
        "name": "2021 Test Channel"
    },
    "recipient": {
        "id": "28:608cacfd-1cea-40c9-b678-4b93e69bb72b",
        "name": "Test Bot"
    },
    "channelData": {
        "settings": {
            "selectedChannel": {
                "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2"
            }
        },
        "team": {
            "aadGroupId": "f3ec8cd2-e704-4344-8c47-9a3a21d683c0",
            "name": "TestTeam2022",
            "id": "19:zFLSDFWsesfzcmKArqKJ-65aOXJz@sgf462H2wz41@thread.tacv2"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "b28fdbfd-2b78-4f93-b0f8-8881793f0f8f"
        }
    }
}
```

Message reçu par votre bot lorsque celui-ci est ajouté à une conversation un-à-un.

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

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_members_added(
 self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
 for member in teams_members_added:
  await turn_context.send_activity(
   MessageFactory.text(f"Welcome your new team member {member.id}")
  )
 return
```

---

### <a name="members-removed"></a>Membres supprimés

Un événement membre supprimé est envoyé à votre bot dans les scénarios suivants :

1. Lorsque le bot lui-même est désinstallé et supprimé d’une conversation.
2. Lorsqu’un utilisateur est supprimé d’une conversation où le bot est installé.

L’activité `eventType` supprimée du membre est définie sur `teamMemberRemoved` le moment où l’événement est envoyé à partir d’un contexte d’équipe. Pour déterminer si le nouveau membre supprimé était le bot lui-même ou un utilisateur, vérifiez l’objet `Activity` du `turnContext`. Si la `MembersRemoved` liste contient un objet où `id` est le même que le `id` champ de l’objet `Recipient` , le membre ajouté est le bot, sinon il s’agit d’un utilisateur. L’ID du bot est mis en forme en tant que `28:<MicrosoftAppId>`.

> [!NOTE]
> Lorsqu’un utilisateur est définitivement supprimé d’un locataire, `membersRemoved conversationUpdate` événement est déclenché.

Le code suivant montre un exemple d’événement de suppression des membres de l’équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersRemovedAsync(IList<ChannelAccount> membersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersRemoved)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // The bot was removed
            // You should clear any cached data you have for this team
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} was removed from {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersRemovedEvent(async (membersRemoved: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            let removedMembers: string = '';
            console.log(JSON.stringify(membersRemoved));
            membersRemoved.forEach((account) => {
                removedMembers += account.id + ' ';
            });
            const name = !teamInfo ? 'not in team' : teamInfo.name;
            const card = CardFactory.heroCard('Account Removed', `${removedMembers} removed from ${teamInfo.name}.`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

L’objet `channelData` dans l’exemple de charge utile suivant est basé sur l’ajout d’un membre à une équipe plutôt qu’à une conversation de groupe, ou sur l’initialisation d’une nouvelle conversation un-à-un :

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

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_members_removed(
 self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
 for member in teams_members_removed:
  await turn_context.send_activity(
   MessageFactory.text(f"Say goodbye to {member.id}")
  )
 return
```

---

### <a name="team-renamed"></a>Équipe renommée

Votre bot est averti lorsque l’équipe est renommée. Il reçoit un événement de `conversationUpdate` avec `eventType.teamRenamed` dans l’objet `channelData` .

Le code suivant montre un exemple d’événement renommé par l’équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamRenamedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team Renamed', `${teamInfo.name} is the new Team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_renamed(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The new team name is {team_info.name}")
 )
```

---

### <a name="team-deleted"></a>Équipe supprimée

Le bot reçoit une notification lorsque l’équipe est supprimée. Il reçoit un `conversationUpdate` événement avec `eventType.teamDeleted` l’objet `channelData` .

Le code suivant montre un exemple d’événement supprimé par l’équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamDeletedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            //handle delete event
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamDeleted",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_deleted(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 //handle delete event
 )
```

---

### <a name="team-restored"></a>Équipe restaurée

Le bot reçoit une notification lorsqu’une équipe est restaurée après sa suppression. Il reçoit un événement de `conversationUpdate` avec `eventType.teamrestored` dans l’objet `channelData` .

Le code suivant montre un exemple d’événement restauré par l’équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamrestoredEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team restored', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamrestored",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_restored(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

### <a name="team-archived"></a>Équipe archivée

Le bot reçoit une notification lorsque l’équipe est installée et archivée. Il reçoit un événement de `conversationUpdate` avec `eventType.teamarchived` dans l’objet `channelData` .

Le code suivant montre un exemple d’événement archivé d’équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamArchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamArchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_archived(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

### <a name="team-unarchived"></a>Équipe non archivée

Le bot reçoit une notification lorsque l’équipe est installée et non archivée. Il reçoit un événement de `conversationUpdate` avec `eventType.teamUnarchived` dans l’objet `channelData` .

Le code suivant montre un exemple d’événement non archivé d’équipe :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamUnarchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamUnarchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_teams_team_unarchived(
 self, team_info: TeamInfo, turn_context: TurnContext
):
 return await turn_context.send_activity(
  MessageFactory.text(f"The team name is {team_info.name}")
 )
```

---

Maintenant que vous avez travaillé avec les événements de mise à jour de conversation, vous pouvez comprendre les événements de réaction de message qui se produisent pour différentes réactions à un message.

## <a name="message-reaction-events"></a>Événements de réaction aux messages

L’événement `messageReaction` est envoyé lorsqu’un utilisateur ajoute ou supprime des réactions à un message, qui a été envoyé par votre bot. Le `replyToId` contient l’ID du message, et le `Type` est le type de réaction au format texte. Les types de réactions sont les suivants : en colère, cœur, rire, genre, triste et surprise. Cet événement ne contient pas le contenu du message d’origine. Si le traitement des réactions à vos messages est important pour votre bot, vous devez stocker les messages lorsque vous les envoyez. Le tableau suivant fournit plus d’informations sur le type d’événement et les objets de charge utile :

| EventType       | Objet de charge utile   | Description                                                             | Portée |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| messageReaction | reactionsAdded   | [Réactions ajoutées au message du bot](#reactions-added-to-bot-message).           | Tous   |
| messageReaction | reactionsRemoved | [Réactions supprimées du message du bot](#reactions-removed-from-bot-message). | Tous |

### <a name="reactions-added-to-bot-message"></a>Réactions ajoutées au message du bot

Le code suivant montre un exemple de réactions à un message de bot :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnReactionsAddedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You reacted with '{reaction.Type}' to the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- Verify -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsAdded(async (context, next) => {
           const reactionsAdded = context.activity.reactionsAdded;
            if (reactionsAdded && reactionsAdded.length > 0) {
                for (let i = 0; i < reactionsAdded.length; i++) {
                    const reaction = reactionsAdded[i];
                    const newReaction = `You reacted with '${reaction.type}' to the following message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}

```

# <a name="json"></a>[JSON](#tab/json)

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
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_reactions_added(
 self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
 for reaction in message_reactions:
  activity = await self._log.find(turn_context.activity.reply_to_id)
  if not activity:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"Activity {turn_context.activity.reply_to_id} not found in log",
   )
  else:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"You added '{reaction.type}' regarding '{activity.text}'",
   )
 return
```

---

### <a name="reactions-removed-from-bot-message"></a>Réactions supprimées du message du bot

Le code suivant montre un exemple de réactions supprimées du message du bot :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnReactionsRemovedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You removed the reaction '{reaction.Type}' from the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

<!-- Verify -->

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsRemoved(async(context,next)=>{
            const reactionsRemoved = context.activity.reactionsRemoved;
            if (reactionsRemoved && reactionsRemoved.length > 0) {
                for (let i = 0; i < reactionsRemoved.length; i++) {
                    const reaction = reactionsRemoved[i];
                    const newReaction = `You removed the reaction '${reaction.type}' from the message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_reactions_removed(
 self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
 for reaction in message_reactions:
  activity = await self._log.find(turn_context.activity.reply_to_id)
  if not activity:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"Activity {turn_context.activity.reply_to_id} not found in log",
   )
  else:
   await self._send_message_and_log_activity_id(
    turn_context,
    f"You removed '{reaction.type}' regarding '{activity.text}'",
   )
 return
```

---

## <a name="installation-update-event"></a>Événement de mise à jour d’installation

Le bot reçoit un événement `installationUpdate` lorsque vous installez un bot sur un thread de conversation. La désinstallation du bot du thread déclenche également l’événement. Lors de l’installation d’un bot, le champ d’**action** de l’événement est défini pour *être ajouté* et, lorsque le bot est désinstallé, le champ **action** est défini pour *être supprimé*.

> [!NOTE]
> Lorsque vous mettez à niveau une application, puis ajoutez ou supprimez un bot, l’action déclenche également l’événement `installationUpdate` . Le champ **d’action** est défini sur *ajouter-mettre à jour* si vous ajoutez un bot ou *supprimer-mettre à jour* si vous supprimez un bot.

### <a name="install-update-event"></a>Installer l’événement de mise à jour

Utilisez l’événement `installationUpdate` pour envoyer un message d’introduction à partir de votre bot lors de l’installation. Cet événement vous aide à répondre à vos exigences en matière de confidentialité et de conservation des données. Vous pouvez également nettoyer et supprimer des données d’utilisateur ou de thread lorsque le bot est désinstallé.

À l’instar de l’événement `conversationUpdate` envoyé lorsque le bot est ajouté à une équipe, le conversation.id de l’événement `installationUpdate` est défini sur l’ID du canal sélectionné par un utilisateur pendant l’installation de l’application ou le canal où l’installation s’est produite. L’ID représente le canal sur lequel l’utilisateur souhaite que le bot fonctionne et doit être utilisé par le bot lors de l’envoi d’un message de bienvenue. Pour les scénarios où l’ID du canal Général est explicitement requis, vous pouvez l’obtenir à `channelData`partir de `team.id` .

Dans cet exemple, les `conversation.id` activités et `installationUpdate` les `conversationUpdate` activités seront définies sur l’ID du canal Response dans l’équipe daves Demo.

![Créer un canal sélectionné](~/assets/videos/addteam.gif)

> [!NOTE]
> L’ID de canal sélectionné est défini uniquement lors de *l’ajout* `installationUpdate` d’événements envoyés lorsqu’une application est installée dans une équipe.

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnInstallationUpdateActivityAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var activity = turnContext.Activity;
    if (string.Equals(activity.Action, "Add", StringComparison.InvariantCultureIgnoreCase))
    {
        // TO:DO Installation workflow
    }
    else
    {
        // TO:DO Uninstallation workflow
    }
    return;
}
```

Vous pouvez également utiliser un gestionnaire dédié pour *ajouter* ou *supprimer* des scénarios comme méthode alternative pour capturer un événement.

```csharp
protected override async Task OnInstallationUpdateAddAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    // TO:DO Installation workflow return;
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
async onInstallationUpdateActivity(context: TurnContext) {
        var activity = context.activity.action;
        if(activity == "Add") {
            await context.sendActivity(MessageFactory.text("Added"));
        }
        else {
            await context.sendActivity(MessageFactory.text("Uninstalled"));
        }
    }
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    {
    "type": "installationUpdate",
    "id": "f:816eb23d-bfa1-afa3-dfeb-d2aa338e9541",
    "timestamp": "2021-11-09T04:47:30.91Z",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1ljv6N86roXr5pjPrCJVIz6xHh5QxjI....",
        "aadObjectId": "eddfa9d4-346e-4cce-a18f-fa6261ad776b"
    },
    "recipient": {
        "id": "28:608cacfd-1cea-40c9-b678-4b93e69bb72b",
        "name": "Test Bot"
    },
    "locale": "en-US",
    "entities": [
        {
            "type": "clientInfo",
            "locale": "en-US"
        }
    ],
    "conversation": {
        "isGroup": true,
        "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2",
        "name": "2021 Test Channel",
        "conversationType": "channel",
        "tenantId": "b28fdbfd-2b78-4f93-b0f8-8881793f0f8f"
    },
    "channelData": {
        "settings": {
            "selectedChannel": {
                "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2"
            }
        },
        "channel": {
            "id": "19:0b7f32667e064dd9b25d7969801541f4@thread.tacv2"
        },
        "team": {
            "aadGroupId": "da849743-4259-475f-ae7a-4f4b0fb49943",
            "name": "TestTeam2022",
            "id": "19:zFLSDFWsesfzcmKArqKJ-65aOXJz@sgf462H2wz41@thread.tacv2"
        },
        "tenant": {
            "id": "b28fdbfd-2b78-4f93-b0f8-8881793f0f8f"
        },
        "source": {
            "name": "message"
        }
    },
    "action": "add"
    }
```

# <a name="python"></a>[Python](#tab/python)

```python
async def on_installation_update(self, turn_context: TurnContext):
   if turn_context.activity.action == "add":   
       await turn_context.send_activity(MessageFactory.text("Added"))
   else:
       await turn_context.send_activity(MessageFactory.text("Uninstalled"))
```

---

## <a name="uninstall-behavior-for-personal-app-with-bot"></a>Comportement de désinstallation pour une application personnelle avec un bot

Lorsque vous désinstallez une application, le bot est également désinstallé. Lorsqu’un utilisateur envoie un message à votre application, il reçoit un code de réponse 403. Votre bot reçoit un code de réponse 403 pour les nouveaux messages publiés par votre bot. Le comportement de post-désinstallation pour les bots dans l’étendue personnelle avec les étendues Teams et groupChat est désormais aligné. Vous ne pouvez pas envoyer ou recevoir de messages après la désinstallation d’une application.

:::image type="content" source="../../../assets/images/bots/uninstallbot.png" alt-text="Désinstaller le code de réponse"lightbox="../../../assets/images/bots/uninstallbot.png"border="true":::

## <a name="event-handling-for-install-and-uninstall-events"></a>Gestion des événements pour les événements d’installation et de désinstallation

Lorsque vous utilisez ces événements d’installation et de désinstallation, il existe certaines instances où les bots accordent des exceptions lors de la réception d’événements inattendus de Teams, ce qui se produit dans les cas suivants :

* Vous générez votre bot sans le kit de développement logiciel (SDK) Microsoft Bot Framework et, par conséquent, le bot donne une exception lors de la réception d’un événement inattendu.
* Vous générez votre bot avec le SDK Microsoft Bot Framework et vous choisissez de modifier le comportement d’événement par défaut en remplaçant le handle d’événement de base.

Il est important de savoir que de nouveaux événements peuvent être ajoutés à tout moment à l’avenir et que votre bot commence à les recevoir. Vous devez donc concevoir la possibilité de recevoir des événements inattendus. Si vous utilisez le Kit de développement logiciel (SDK) Bot Framework, votre bot répond automatiquement avec un 200 : OK pour tous les événements que vous ne choisissez pas de gérer.

## <a name="code-sample"></a>Exemple de code

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|----------|-----------------|----------|
| Bot de conversation | Exemple de code pour les événements de conversation de bots. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)  | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Envoyer des messages proactifs](~/bots/how-to/conversations/send-proactive-messages.md)
