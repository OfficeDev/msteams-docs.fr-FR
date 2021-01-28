---
title: S’abonner à des événements de conversation
author: WashingtonKayaker
description: Comment s’abonner à des événements de conversation à partir de votre bot Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: b4dc70e4619043bd0b675206770093b086fc5ec6
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014319"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="afde4-103">S’abonner à des événements de conversation</span><span class="sxs-lookup"><span data-stu-id="afde4-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="afde4-104">Microsoft Teams envoie des notifications à votre robot pour les événements qui se produisent dans les zones où il est actif.</span><span class="sxs-lookup"><span data-stu-id="afde4-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="afde4-105">Vous pouvez capturer ces événements dans votre code et prendre des mesures les concernant, notamment les suivants :</span><span class="sxs-lookup"><span data-stu-id="afde4-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="afde4-106">Déclencher un message de bienvenue lorsque votre bot est ajouté à une équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="afde4-107">Déclencher un message de bienvenue lorsqu’un nouveau membre d’équipe est ajouté ou supprimé</span><span class="sxs-lookup"><span data-stu-id="afde4-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="afde4-108">Déclencher une notification lorsqu’un canal est créé, renommé ou supprimé</span><span class="sxs-lookup"><span data-stu-id="afde4-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="afde4-109">Lorsqu’un message bot est aimé par un utilisateur</span><span class="sxs-lookup"><span data-stu-id="afde4-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="afde4-110">Événements de mise à jour de conversation</span><span class="sxs-lookup"><span data-stu-id="afde4-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="afde4-111">De nouveaux événements peuvent être ajoutés à tout moment et votre bot commence à les recevoir.</span><span class="sxs-lookup"><span data-stu-id="afde4-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="afde4-112">Vous devez concevoir la possibilité de recevoir des événements inattendus.</span><span class="sxs-lookup"><span data-stu-id="afde4-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="afde4-113">Si vous utilisez le SDK Bot Framework, votre bot répond automatiquement à tous les événements que vous ne `200 - OK` choisissez pas de gérer.</span><span class="sxs-lookup"><span data-stu-id="afde4-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="afde4-114">Un robot reçoit un événement `conversationUpdate` une fois qu’il a été ajouté à une conversation, les autres membres ont été ajoutés à une conversation ou supprimés de celle-ci, ou les métadonnées de conversation ont changé.</span><span class="sxs-lookup"><span data-stu-id="afde4-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="afde4-115">L’événement `conversationUpdate` est envoyé à votre robot lorsqu’il reçoit des informations sur les mises à jour d’appartenance pour les équipes dans lesquelles il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="afde4-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="afde4-116">Il reçoit également une mise à jour lorsqu’il a été ajouté pour la première fois, spécifiquement pour les conversations personnelles.</span><span class="sxs-lookup"><span data-stu-id="afde4-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="afde4-117">Le tableau suivant présente la liste des événements de mise à jour de conversation Teams, avec des liens vers plus de détails.</span><span class="sxs-lookup"><span data-stu-id="afde4-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="afde4-118">Action Taken</span><span class="sxs-lookup"><span data-stu-id="afde4-118">Action Taken</span></span>        | <span data-ttu-id="afde4-119">EventType</span><span class="sxs-lookup"><span data-stu-id="afde4-119">EventType</span></span>         | <span data-ttu-id="afde4-120">Méthode Appelée</span><span class="sxs-lookup"><span data-stu-id="afde4-120">Method Called</span></span>              | <span data-ttu-id="afde4-121">Description</span><span class="sxs-lookup"><span data-stu-id="afde4-121">Description</span></span>                | <span data-ttu-id="afde4-122">Portée</span><span class="sxs-lookup"><span data-stu-id="afde4-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="afde4-123">canal créé</span><span class="sxs-lookup"><span data-stu-id="afde4-123">channel created</span></span>     | <span data-ttu-id="afde4-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="afde4-124">channelCreated</span></span>    | <span data-ttu-id="afde4-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="afde4-126">Un canal a été créé</span><span class="sxs-lookup"><span data-stu-id="afde4-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="afde4-127">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-127">Team</span></span> |
| <span data-ttu-id="afde4-128">canal renommé</span><span class="sxs-lookup"><span data-stu-id="afde4-128">channel renamed</span></span>     | <span data-ttu-id="afde4-129">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="afde4-129">channelRenamed</span></span>    | <span data-ttu-id="afde4-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="afde4-131">Un canal a été renommé</span><span class="sxs-lookup"><span data-stu-id="afde4-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="afde4-132">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-132">Team</span></span> |
| <span data-ttu-id="afde4-133">canal supprimé</span><span class="sxs-lookup"><span data-stu-id="afde4-133">channel deleted</span></span>     | <span data-ttu-id="afde4-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="afde4-134">channelDeleted</span></span>    | <span data-ttu-id="afde4-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="afde4-136">Un canal a été supprimé</span><span class="sxs-lookup"><span data-stu-id="afde4-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="afde4-137">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-137">Team</span></span> |
| <span data-ttu-id="afde4-138">canal restauré</span><span class="sxs-lookup"><span data-stu-id="afde4-138">channel restored</span></span>    | <span data-ttu-id="afde4-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="afde4-139">channelRestored</span></span>    | <span data-ttu-id="afde4-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="afde4-141">Un canal a été restauré</span><span class="sxs-lookup"><span data-stu-id="afde4-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="afde4-142">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-142">Team</span></span> |
| <span data-ttu-id="afde4-143">membres ajoutés</span><span class="sxs-lookup"><span data-stu-id="afde4-143">members added</span></span>   | <span data-ttu-id="afde4-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="afde4-144">membersAdded</span></span>   | <span data-ttu-id="afde4-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="afde4-146">Un membre ajouté</span><span class="sxs-lookup"><span data-stu-id="afde4-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="afde4-147">Tous</span><span class="sxs-lookup"><span data-stu-id="afde4-147">All</span></span> |
| <span data-ttu-id="afde4-148">membres supprimés</span><span class="sxs-lookup"><span data-stu-id="afde4-148">members removed</span></span> | <span data-ttu-id="afde4-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="afde4-149">membersRemoved</span></span> | <span data-ttu-id="afde4-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="afde4-151">Un membre a été supprimé</span><span class="sxs-lookup"><span data-stu-id="afde4-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="afde4-152">équipe & groupChat</span><span class="sxs-lookup"><span data-stu-id="afde4-152">groupChat & team</span></span> |
| <span data-ttu-id="afde4-153">équipe renommée</span><span class="sxs-lookup"><span data-stu-id="afde4-153">team renamed</span></span>        | <span data-ttu-id="afde4-154">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="afde4-154">teamRenamed</span></span>       | <span data-ttu-id="afde4-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="afde4-156">Une équipe a été renommée</span><span class="sxs-lookup"><span data-stu-id="afde4-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="afde4-157">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-157">Team</span></span> |
| <span data-ttu-id="afde4-158">équipe supprimée</span><span class="sxs-lookup"><span data-stu-id="afde4-158">team deleted</span></span>        | <span data-ttu-id="afde4-159">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="afde4-159">teamDeleted</span></span>       | <span data-ttu-id="afde4-160">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-160">OnTeamsTeamDeletedAsync</span></span>    | [<span data-ttu-id="afde4-161">Une équipe a été supprimée</span><span class="sxs-lookup"><span data-stu-id="afde4-161">A Team was deleted</span></span>](#team-deleted)       | <span data-ttu-id="afde4-162">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-162">Team</span></span> |
| <span data-ttu-id="afde4-163">équipe archivée</span><span class="sxs-lookup"><span data-stu-id="afde4-163">team archived</span></span>        | <span data-ttu-id="afde4-164">teamArchived</span><span class="sxs-lookup"><span data-stu-id="afde4-164">teamArchived</span></span>       | <span data-ttu-id="afde4-165">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-165">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="afde4-166">Une équipe a été archivée</span><span class="sxs-lookup"><span data-stu-id="afde4-166">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="afde4-167">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-167">Team</span></span> |
| <span data-ttu-id="afde4-168">équipe nonarchived</span><span class="sxs-lookup"><span data-stu-id="afde4-168">team unarchived</span></span>        | <span data-ttu-id="afde4-169">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="afde4-169">teamUnarchived</span></span>       | <span data-ttu-id="afde4-170">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-170">OnTeamsTeamUnarchivedAsync</span></span>    | [<span data-ttu-id="afde4-171">Une équipe n’a pas étéarchive</span><span class="sxs-lookup"><span data-stu-id="afde4-171">A Team was unarchived</span></span>](#team-unarchived)       | <span data-ttu-id="afde4-172">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-172">Team</span></span> |
| <span data-ttu-id="afde4-173">équipe restaurée</span><span class="sxs-lookup"><span data-stu-id="afde4-173">team restored</span></span>        | <span data-ttu-id="afde4-174">teamRestored</span><span class="sxs-lookup"><span data-stu-id="afde4-174">teamRestored</span></span>      | <span data-ttu-id="afde4-175">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="afde4-175">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="afde4-176">Une équipe a été restaurée</span><span class="sxs-lookup"><span data-stu-id="afde4-176">A Team was restored</span></span>](#team-restored)       | <span data-ttu-id="afde4-177">Équipe</span><span class="sxs-lookup"><span data-stu-id="afde4-177">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="afde4-178">Canal créé</span><span class="sxs-lookup"><span data-stu-id="afde4-178">Channel created</span></span>

<span data-ttu-id="afde4-179">L’événement créé par le canal est envoyé à votre bot chaque fois qu’un nouveau canal est créé dans une équipe où votre bot est installé.</span><span class="sxs-lookup"><span data-stu-id="afde4-179">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-180">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-181">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-181">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-182">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-182">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-183">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-183">Python</span></span>](#tab/python)

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

* * *

### <a name="channel-renamed"></a><span data-ttu-id="afde4-184">Canal renommé</span><span class="sxs-lookup"><span data-stu-id="afde4-184">Channel renamed</span></span>

<span data-ttu-id="afde4-185">L’événement renommé de canal est envoyé à votre bot chaque fois qu’un canal est renommé dans une équipe où votre bot est installé.</span><span class="sxs-lookup"><span data-stu-id="afde4-185">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-186">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-186">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-187">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-187">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-188">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-189">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-189">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="afde4-190">Canal supprimé</span><span class="sxs-lookup"><span data-stu-id="afde4-190">Channel Deleted</span></span>

<span data-ttu-id="afde4-191">L’événement de canal supprimé est envoyé à votre bot chaque fois qu’un canal est supprimé dans une équipe où votre bot est installé.</span><span class="sxs-lookup"><span data-stu-id="afde4-191">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-193">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-194">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-194">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-195">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-195">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="afde4-196">Canal restauré</span><span class="sxs-lookup"><span data-stu-id="afde4-196">Channel restored</span></span>

<span data-ttu-id="afde4-197">L’événement de restauration de canal est envoyé à votre bot chaque fois qu’un canal précédemment supprimé est restauré dans une équipe dans qui votre bot est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="afde4-197">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-199">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-199">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-200">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-200">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-201">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-201">Python</span></span>](#tab/python)

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

* * *

### <a name="team-members-added"></a><span data-ttu-id="afde4-202">Membres d’équipe ajoutés</span><span class="sxs-lookup"><span data-stu-id="afde4-202">Team members added</span></span>

<span data-ttu-id="afde4-203">L’événement est envoyé à votre bot la première fois qu’il est ajouté à une conversation et chaque fois qu’un nouvel utilisateur est ajouté à une conversation d’équipe ou de groupe dans qui votre `teamMemberAdded` bot est installé.</span><span class="sxs-lookup"><span data-stu-id="afde4-203">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="afde4-204">Les informations utilisateur (ID) sont uniques pour votre bot et peuvent être mises en cache pour une utilisation future par votre service (par exemple, l’envoi d’un message à un utilisateur spécifique).</span><span class="sxs-lookup"><span data-stu-id="afde4-204">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-205">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-205">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-206">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-206">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-207">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-207">JSON</span></span>](#tab/json)

<span data-ttu-id="afde4-208">Il s’agit du message que votre bot reçoit lorsque le bot est ajouté **à une équipe.**</span><span class="sxs-lookup"><span data-stu-id="afde4-208">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="afde4-209">Il s’agit du message que votre bot reçoit lorsque le bot est ajouté \* à une conversation *un-à-un.*</span><span class="sxs-lookup"><span data-stu-id="afde4-209">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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
    "aadObjectId": "**_"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "_*_"
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

# <a name="python"></a>[<span data-ttu-id="afde4-210">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-210">Python</span></span>](#tab/python)

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

<span data-ttu-id="afde4-211">_ \* \*</span><span class="sxs-lookup"><span data-stu-id="afde4-211">_ \* \*</span></span>

### <a name="team-members-removed"></a><span data-ttu-id="afde4-212">Membres d’équipe supprimés</span><span class="sxs-lookup"><span data-stu-id="afde4-212">Team members removed</span></span>

<span data-ttu-id="afde4-213">L’événement est envoyé à votre bot s’il est supprimé d’une équipe et chaque fois qu’un utilisateur est supprimé d’une équipe dont il `teamMemberRemoved` est membre.</span><span class="sxs-lookup"><span data-stu-id="afde4-213">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="afde4-214">Vous pouvez déterminer si le nouveau membre supprimé était le bot lui-même ou un utilisateur en regardant `Activity` l’objet du `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="afde4-214">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="afde4-215">Si le champ de l’objet est identique au champ de l’objet, le membre supprimé est le bot, sinon, il s’agit `Id` `MembersRemoved` `Id` `Recipient` d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="afde4-215">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="afde4-216">Le bot est `Id` généralement : `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="afde4-216">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="afde4-217">Lorsqu’un utilisateur est supprimé définitivement d’un client, `membersRemoved conversationUpdate` l’événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="afde4-217">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-218">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-218">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-219">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-219">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-220">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-220">JSON</span></span>](#tab/json)

<span data-ttu-id="afde4-221">L’objet de l’exemple de charge utile suivant est basé sur l’ajout d’un membre à une équipe plutôt qu’à une conversation de groupe ou sur le début d’une nouvelle `channelData` conversation un-à-un :</span><span class="sxs-lookup"><span data-stu-id="afde4-221">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="afde4-222">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-222">Python</span></span>](#tab/python)

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

* * *

### <a name="team-renamed"></a><span data-ttu-id="afde4-223">Équipe renommée</span><span class="sxs-lookup"><span data-stu-id="afde4-223">Team renamed</span></span>

<span data-ttu-id="afde4-224">Votre bot est averti lorsque l’équipe dans qui il se trouve a été renommé.</span><span class="sxs-lookup"><span data-stu-id="afde4-224">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="afde4-225">Il reçoit un `conversationUpdate` événement avec `eventType.teamRenamed` dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="afde4-225">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-226">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-226">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-227">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-227">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-228">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-228">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-229">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-229">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="afde4-230">Équipe supprimée</span><span class="sxs-lookup"><span data-stu-id="afde4-230">Team deleted</span></span>

<span data-ttu-id="afde4-231">Votre bot est averti lorsque l’équipe dans qui elle se trouve a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="afde4-231">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="afde4-232">Il reçoit un `conversationUpdate` événement avec `eventType.teamDeleted` dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="afde4-232">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-233">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-233">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-234">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-234">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-235">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-235">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-236">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-236">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="afde4-237">Équipe restaurée</span><span class="sxs-lookup"><span data-stu-id="afde4-237">Team restored</span></span>

<span data-ttu-id="afde4-238">Le bot reçoit une notification lorsqu’il est restauré à partir de la suppression.</span><span class="sxs-lookup"><span data-stu-id="afde4-238">The bot receives a notification when it is restored from deletion.</span></span> <span data-ttu-id="afde4-239">Il reçoit un `conversationUpdate` événement avec `eventType.teamrestored` dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="afde4-239">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-240">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-240">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-241">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-241">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-242">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-242">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-243">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-243">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="afde4-244">Équipe archivée</span><span class="sxs-lookup"><span data-stu-id="afde4-244">Team archived</span></span>

<span data-ttu-id="afde4-245">Le bot reçoit une notification lorsque l’équipe dans qui il est installé est archivée.</span><span class="sxs-lookup"><span data-stu-id="afde4-245">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="afde4-246">Il reçoit un `conversationUpdate` événement avec `eventType.teamarchived` dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="afde4-246">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-247">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-247">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-248">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-248">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-249">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-249">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-250">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="afde4-251">Équipe nonarchived</span><span class="sxs-lookup"><span data-stu-id="afde4-251">Team unarchived</span></span>

<span data-ttu-id="afde4-252">Le bot reçoit une notification lorsque l’équipe dans qui il est installé n’est pasarchive.</span><span class="sxs-lookup"><span data-stu-id="afde4-252">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="afde4-253">Il reçoit un `conversationUpdate` événement avec `eventType.teamUnarchived` dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="afde4-253">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-254">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-254">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-255">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-255">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-256">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-256">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-257">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-257">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="afde4-258">Événements de réaction aux messages</span><span class="sxs-lookup"><span data-stu-id="afde4-258">Message reaction events</span></span>

<span data-ttu-id="afde4-259">L’événement est envoyé lorsqu’un utilisateur ajoute ou supprime des réactions à un message envoyé `messageReaction` par votre bot.</span><span class="sxs-lookup"><span data-stu-id="afde4-259">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="afde4-260">Contient l’ID du message spécifique et le type de réaction au `replyToId` `Type` format texte.</span><span class="sxs-lookup"><span data-stu-id="afde4-260">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="afde4-261">Les types de réactions sont les suivants : « heart », « heart », « like », « Sad », « surprised ».</span><span class="sxs-lookup"><span data-stu-id="afde4-261">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="afde4-262">Cet événement ne contient pas le contenu du message d’origine, donc si le traitement des réactions à vos messages est important pour votre bot, vous devrez stocker les messages lorsque vous les envoyez.</span><span class="sxs-lookup"><span data-stu-id="afde4-262">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="afde4-263">EventType</span><span class="sxs-lookup"><span data-stu-id="afde4-263">EventType</span></span>       | <span data-ttu-id="afde4-264">Objet Payload</span><span class="sxs-lookup"><span data-stu-id="afde4-264">Payload object</span></span>   | <span data-ttu-id="afde4-265">Description</span><span class="sxs-lookup"><span data-stu-id="afde4-265">Description</span></span>                                                             | <span data-ttu-id="afde4-266">Portée</span><span class="sxs-lookup"><span data-stu-id="afde4-266">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="afde4-267">messageReaction</span><span class="sxs-lookup"><span data-stu-id="afde4-267">messageReaction</span></span> | <span data-ttu-id="afde4-268">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="afde4-268">reactionsAdded</span></span>   | [<span data-ttu-id="afde4-269">Réaction au message du bot</span><span class="sxs-lookup"><span data-stu-id="afde4-269">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="afde4-270">Tous</span><span class="sxs-lookup"><span data-stu-id="afde4-270">All</span></span>   |
| <span data-ttu-id="afde4-271">messageReaction</span><span class="sxs-lookup"><span data-stu-id="afde4-271">messageReaction</span></span> | <span data-ttu-id="afde4-272">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="afde4-272">reactionsRemoved</span></span> | [<span data-ttu-id="afde4-273">Réaction supprimée du message du bot</span><span class="sxs-lookup"><span data-stu-id="afde4-273">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="afde4-274">Tous</span><span class="sxs-lookup"><span data-stu-id="afde4-274">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="afde4-275">Réactions à un message de bot</span><span class="sxs-lookup"><span data-stu-id="afde4-275">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-276">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-276">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-277">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-277">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-278">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-278">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-279">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-279">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="afde4-280">Réactions supprimées du message du bot</span><span class="sxs-lookup"><span data-stu-id="afde4-280">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="afde4-281">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="afde4-281">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="afde4-282">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="afde4-282">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afde4-283">JSON</span><span class="sxs-lookup"><span data-stu-id="afde4-283">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afde4-284">Python</span><span class="sxs-lookup"><span data-stu-id="afde4-284">Python</span></span>](#tab/python)

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

## <a name="samples"></a><span data-ttu-id="afde4-285">Exemples</span><span class="sxs-lookup"><span data-stu-id="afde4-285">Samples</span></span>
<span data-ttu-id="afde4-286">Pour obtenir un exemple de code montrant les événements de conversation de bots, voir :</span><span class="sxs-lookup"><span data-stu-id="afde4-286">For sample code showing the bots conversation events, see:</span></span>

[<span data-ttu-id="afde4-287">Exemple d’événements de conversation de bots Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="afde4-287">Microsoft Teams bots conversation events sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)



