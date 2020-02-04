---
title: S’abonner à des événements de conversation
author: WashingtonKayaker
description: Comment s’abonner à des événements de conversation à partir de votre robot Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: a8c6c39989a7d09a325412438f0d2ace78259cb7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673936"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="9709e-103">S’abonner à des événements de conversation</span><span class="sxs-lookup"><span data-stu-id="9709e-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="9709e-104">Microsoft teams envoie des notifications à votre bot pour les événements qui se produisent dans les étendues où votre bot est actif.</span><span class="sxs-lookup"><span data-stu-id="9709e-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="9709e-105">Vous pouvez capturer ces événements dans votre code et agir sur ceux-ci, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="9709e-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="9709e-106">Déclencher un message de bienvenue lorsque votre bot est ajouté à une équipe</span><span class="sxs-lookup"><span data-stu-id="9709e-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="9709e-107">Déclencher un message de bienvenue lors de l’ajout ou de la suppression d’un nouveau membre d’équipe</span><span class="sxs-lookup"><span data-stu-id="9709e-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="9709e-108">Déclencher une notification lorsqu’un canal est créé, renommé ou supprimé</span><span class="sxs-lookup"><span data-stu-id="9709e-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="9709e-109">Quand un message bot est aimé par un utilisateur</span><span class="sxs-lookup"><span data-stu-id="9709e-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="9709e-110">Événements de mise à jour de conversation</span><span class="sxs-lookup"><span data-stu-id="9709e-110">Conversation update events</span></span>

<span data-ttu-id="9709e-111">Un bot reçoit un `conversationUpdate` événement lorsqu’il a été ajouté à une conversation, d’autres membres ont été ajoutés à une conversation ou en étant supprimés, ou les métadonnées de conversation ont changé.</span><span class="sxs-lookup"><span data-stu-id="9709e-111">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="9709e-112">L' `conversationUpdate` événement est envoyé à votre bot lorsqu’il reçoit des informations sur les mises à jour d’appartenance de teams dans lesquelles il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="9709e-112">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="9709e-113">Elle reçoit également une mise à jour lorsqu’elle a été ajoutée pour la première fois spécifiquement pour les conversations personnelles.</span><span class="sxs-lookup"><span data-stu-id="9709e-113">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="9709e-114">Le tableau suivant présente la liste des événements de mise à jour de conversation de teams, avec des liens vers des informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="9709e-114">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="9709e-115">Action entreprise</span><span class="sxs-lookup"><span data-stu-id="9709e-115">Action Taken</span></span>        | <span data-ttu-id="9709e-116">EventType</span><span class="sxs-lookup"><span data-stu-id="9709e-116">EventType</span></span>         | <span data-ttu-id="9709e-117">Méthode appelée</span><span class="sxs-lookup"><span data-stu-id="9709e-117">Method Called</span></span>              | <span data-ttu-id="9709e-118">Description</span><span class="sxs-lookup"><span data-stu-id="9709e-118">Description</span></span>                | <span data-ttu-id="9709e-119">Portée</span><span class="sxs-lookup"><span data-stu-id="9709e-119">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="9709e-120">canal créé</span><span class="sxs-lookup"><span data-stu-id="9709e-120">channel created</span></span>     | <span data-ttu-id="9709e-121">channelCreated</span><span class="sxs-lookup"><span data-stu-id="9709e-121">channelCreated</span></span>    | <span data-ttu-id="9709e-122">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="9709e-122">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="9709e-123">Un canal a été créé</span><span class="sxs-lookup"><span data-stu-id="9709e-123">A channel was created</span></span>](#channel-created) | <span data-ttu-id="9709e-124">Équipe</span><span class="sxs-lookup"><span data-stu-id="9709e-124">Team</span></span> |
| <span data-ttu-id="9709e-125">canal renommé</span><span class="sxs-lookup"><span data-stu-id="9709e-125">channel renamed</span></span>     | <span data-ttu-id="9709e-126">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="9709e-126">channelRenamed</span></span>    | <span data-ttu-id="9709e-127">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="9709e-127">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="9709e-128">Un canal a été renommé.</span><span class="sxs-lookup"><span data-stu-id="9709e-128">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="9709e-129">Équipe</span><span class="sxs-lookup"><span data-stu-id="9709e-129">Team</span></span> |
| <span data-ttu-id="9709e-130">canal supprimé</span><span class="sxs-lookup"><span data-stu-id="9709e-130">channel deleted</span></span>     | <span data-ttu-id="9709e-131">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="9709e-131">channelDeleted</span></span>    | <span data-ttu-id="9709e-132">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="9709e-132">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="9709e-133">Un canal a été supprimé</span><span class="sxs-lookup"><span data-stu-id="9709e-133">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="9709e-134">Équipe</span><span class="sxs-lookup"><span data-stu-id="9709e-134">Team</span></span> |
| <span data-ttu-id="9709e-135">membres d’équipe ajoutés</span><span class="sxs-lookup"><span data-stu-id="9709e-135">team members added</span></span>   | <span data-ttu-id="9709e-136">teamMemberAdded</span><span class="sxs-lookup"><span data-stu-id="9709e-136">teamMemberAdded</span></span>   | <span data-ttu-id="9709e-137">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="9709e-137">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="9709e-138">Un membre ajouté à Team</span><span class="sxs-lookup"><span data-stu-id="9709e-138">A Member added to team</span></span>](#team-members-added)   | <span data-ttu-id="9709e-139">Tous</span><span class="sxs-lookup"><span data-stu-id="9709e-139">All</span></span> |
| <span data-ttu-id="9709e-140">membres d’équipe supprimés</span><span class="sxs-lookup"><span data-stu-id="9709e-140">team members removed</span></span> | <span data-ttu-id="9709e-141">teamMemberRemoved</span><span class="sxs-lookup"><span data-stu-id="9709e-141">teamMemberRemoved</span></span> | <span data-ttu-id="9709e-142">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="9709e-142">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="9709e-143">Un membre a été supprimé de Team</span><span class="sxs-lookup"><span data-stu-id="9709e-143">A Member was removed from team</span></span>](#team-members-removed) | <span data-ttu-id="9709e-144">équipe de & groupChat</span><span class="sxs-lookup"><span data-stu-id="9709e-144">groupChat & team</span></span> |
| <span data-ttu-id="9709e-145">équipe renommée</span><span class="sxs-lookup"><span data-stu-id="9709e-145">team renamed</span></span>        | <span data-ttu-id="9709e-146">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="9709e-146">teamRenamed</span></span>       | <span data-ttu-id="9709e-147">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="9709e-147">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="9709e-148">Une équipe a été renommée</span><span class="sxs-lookup"><span data-stu-id="9709e-148">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="9709e-149">Équipe</span><span class="sxs-lookup"><span data-stu-id="9709e-149">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="9709e-150">Canal créé</span><span class="sxs-lookup"><span data-stu-id="9709e-150">Channel created</span></span>

<span data-ttu-id="9709e-151">L’événement de canal créé est envoyé à votre bot chaque fois qu’un nouveau canal est créé dans une équipe dans laquelle votre robot est installé.</span><span class="sxs-lookup"><span data-stu-id="9709e-151">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9709e-152">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9709e-152">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9709e-153">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="9709e-153">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="9709e-154">JSON</span><span class="sxs-lookup"><span data-stu-id="9709e-154">JSON</span></span>](#tab/json)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="9709e-155">Python</span><span class="sxs-lookup"><span data-stu-id="9709e-155">Python</span></span>](#tab/python)

```python
async def on_teams_channel_created_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="channel-renamed"></a><span data-ttu-id="9709e-156">Canal renommé</span><span class="sxs-lookup"><span data-stu-id="9709e-156">Channel renamed</span></span>

<span data-ttu-id="9709e-157">L’événement de renommée de canal est envoyé à votre bot chaque fois qu’un canal est renommé dans une équipe dans laquelle le robot est installé.</span><span class="sxs-lookup"><span data-stu-id="9709e-157">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9709e-158">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9709e-158">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9709e-159">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="9709e-159">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="9709e-160">JSON</span><span class="sxs-lookup"><span data-stu-id="9709e-160">JSON</span></span>](#tab/json)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="9709e-161">Python</span><span class="sxs-lookup"><span data-stu-id="9709e-161">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="9709e-162">Canal supprimé</span><span class="sxs-lookup"><span data-stu-id="9709e-162">Channel Deleted</span></span>

<span data-ttu-id="9709e-163">L’événement de canal Deleted est envoyé à votre bot chaque fois qu’un canal est supprimé dans une équipe dans laquelle le robot est installé.</span><span class="sxs-lookup"><span data-stu-id="9709e-163">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9709e-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9709e-164">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9709e-165">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="9709e-165">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="9709e-166">JSON</span><span class="sxs-lookup"><span data-stu-id="9709e-166">JSON</span></span>](#tab/json)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="9709e-167">Python</span><span class="sxs-lookup"><span data-stu-id="9709e-167">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="9709e-168">Membres d’équipe ajoutés</span><span class="sxs-lookup"><span data-stu-id="9709e-168">Team members added</span></span>

<span data-ttu-id="9709e-169">L' `teamMemberAdded` événement est envoyé à votre robot la première fois qu’il est ajouté à une conversation et chaque fois qu’un nouvel utilisateur est ajouté à une équipe ou à une conversation de groupe dans laquelle votre robot est installé.</span><span class="sxs-lookup"><span data-stu-id="9709e-169">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="9709e-170">Les informations utilisateur (ID) sont uniques pour votre robot et peuvent être mises en cache pour une utilisation future par votre service (par exemple, l’envoi d’un message à un utilisateur spécifique).</span><span class="sxs-lookup"><span data-stu-id="9709e-170">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9709e-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9709e-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<ChannelAccount> membersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersAdded)
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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9709e-172">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="9709e-172">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="9709e-173">JSON</span><span class="sxs-lookup"><span data-stu-id="9709e-173">JSON</span></span>](#tab/json)

<span data-ttu-id="9709e-174">Il s’agit du message que votre robot reçoit lorsque le bot est ajouté **à une équipe**.</span><span class="sxs-lookup"><span data-stu-id="9709e-174">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="9709e-175">Il s’agit du message que votre bot recevra lorsque le bot est ajouté*à une conversation un-à-* un.</span><span class="sxs-lookup"><span data-stu-id="9709e-175">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="pythontabpython"></a>[<span data-ttu-id="9709e-176">Python</span><span class="sxs-lookup"><span data-stu-id="9709e-176">Python</span></span>](#tab/python)

```python
async def on_teams_members_added_activity(
    self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(
            MessageFactory.text(f"Welcome your new team member {member.id}")
        )
    return
```

* * *

### <a name="team-members-removed"></a><span data-ttu-id="9709e-177">Membres d’équipe supprimés</span><span class="sxs-lookup"><span data-stu-id="9709e-177">Team members removed</span></span>

<span data-ttu-id="9709e-178">L' `teamMemberRemoved` événement est envoyé à votre bot s’il est supprimé d’une équipe et chaque fois qu’un utilisateur est supprimé d’une équipe dont votre robot est membre.</span><span class="sxs-lookup"><span data-stu-id="9709e-178">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="9709e-179">Vous pouvez déterminer si le nouveau membre supprimé était le robot lui-même ou un utilisateur en examinant l' `Activity` objet `turnContext`du.</span><span class="sxs-lookup"><span data-stu-id="9709e-179">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="9709e-180">Si le `Id` champ de l' `MembersRemoved` objet est le même que le `Id` champ de l' `Recipient` objet, le membre supprimé est le bot, sinon il s’agit d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9709e-180">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise it is a user.</span></span>  <span data-ttu-id="9709e-181">Les robots `Id` seront généralement :`28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="9709e-181">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9709e-182">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9709e-182">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9709e-183">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="9709e-183">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="9709e-184">JSON</span><span class="sxs-lookup"><span data-stu-id="9709e-184">JSON</span></span>](#tab/json)

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


# <a name="pythontabpython"></a>[<span data-ttu-id="9709e-185">Python</span><span class="sxs-lookup"><span data-stu-id="9709e-185">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed_activity(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to your team member {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="9709e-186">Équipe renommée</span><span class="sxs-lookup"><span data-stu-id="9709e-186">Team renamed</span></span>

<span data-ttu-id="9709e-187">Votre robot est informé de la modification du nom de l’équipe dans laquelle il se trouve.</span><span class="sxs-lookup"><span data-stu-id="9709e-187">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="9709e-188">Elle reçoit un `conversationUpdate` événement avec `eventType.teamRenamed` dans l' `channelData` objet.</span><span class="sxs-lookup"><span data-stu-id="9709e-188">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9709e-189">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9709e-189">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9709e-190">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="9709e-190">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="9709e-191">JSON</span><span class="sxs-lookup"><span data-stu-id="9709e-191">JSON</span></span>](#tab/json)

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


# <a name="pythontabpython"></a>[<span data-ttu-id="9709e-192">Python</span><span class="sxs-lookup"><span data-stu-id="9709e-192">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed_activity(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="9709e-193">Événements de réaction de message</span><span class="sxs-lookup"><span data-stu-id="9709e-193">Message reaction events</span></span>

<span data-ttu-id="9709e-194">L' `messageReaction` événement est envoyé lorsqu’un utilisateur ajoute ou supprime des réactions à un message qui a été envoyé par votre bot.</span><span class="sxs-lookup"><span data-stu-id="9709e-194">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="9709e-195">Le `replyToId` contient l’ID du message spécifique et le `Type` est le type de réaction au format texte.</span><span class="sxs-lookup"><span data-stu-id="9709e-195">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="9709e-196">Les types de réactions sont les suivants : « en colère », « coeur », « rire », « comme », « triste », « surpris ».</span><span class="sxs-lookup"><span data-stu-id="9709e-196">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="9709e-197">Cet événement ne contient pas le contenu du message d’origine, donc si le traitement des réactions à vos messages est important pour votre robot, vous devrez stocker les messages lorsque vous les envoyez.</span><span class="sxs-lookup"><span data-stu-id="9709e-197">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="9709e-198">EventType</span><span class="sxs-lookup"><span data-stu-id="9709e-198">EventType</span></span>       | <span data-ttu-id="9709e-199">Objet Payload</span><span class="sxs-lookup"><span data-stu-id="9709e-199">Payload object</span></span>   | <span data-ttu-id="9709e-200">Description</span><span class="sxs-lookup"><span data-stu-id="9709e-200">Description</span></span>                                                             | <span data-ttu-id="9709e-201">Portée</span><span class="sxs-lookup"><span data-stu-id="9709e-201">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="9709e-202">messageReaction</span><span class="sxs-lookup"><span data-stu-id="9709e-202">messageReaction</span></span> | <span data-ttu-id="9709e-203">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="9709e-203">reactionsAdded</span></span>   | [<span data-ttu-id="9709e-204">Message de réaction au bot</span><span class="sxs-lookup"><span data-stu-id="9709e-204">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="9709e-205">Tous</span><span class="sxs-lookup"><span data-stu-id="9709e-205">All</span></span>   |
| <span data-ttu-id="9709e-206">messageReaction</span><span class="sxs-lookup"><span data-stu-id="9709e-206">messageReaction</span></span> | <span data-ttu-id="9709e-207">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="9709e-207">reactionsRemoved</span></span> | [<span data-ttu-id="9709e-208">Réaction supprimée du message bot</span><span class="sxs-lookup"><span data-stu-id="9709e-208">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="9709e-209">Tous</span><span class="sxs-lookup"><span data-stu-id="9709e-209">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="9709e-210">Réactions à un message bot</span><span class="sxs-lookup"><span data-stu-id="9709e-210">Reactions to a bot message</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9709e-211">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9709e-211">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9709e-212">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="9709e-212">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="9709e-213">JSON</span><span class="sxs-lookup"><span data-stu-id="9709e-213">JSON</span></span>](#tab/json)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="9709e-214">Python</span><span class="sxs-lookup"><span data-stu-id="9709e-214">Python</span></span>](#tab/python)

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

* * *

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="9709e-215">Réactions supprimées du message bot</span><span class="sxs-lookup"><span data-stu-id="9709e-215">Reactions removed from bot message</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="9709e-216">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="9709e-216">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="9709e-217">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="9709e-217">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="jsontabjson"></a>[<span data-ttu-id="9709e-218">JSON</span><span class="sxs-lookup"><span data-stu-id="9709e-218">JSON</span></span>](#tab/json)

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

# <a name="pythontabpython"></a>[<span data-ttu-id="9709e-219">Python</span><span class="sxs-lookup"><span data-stu-id="9709e-219">Python</span></span>](#tab/python)

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

* * *
