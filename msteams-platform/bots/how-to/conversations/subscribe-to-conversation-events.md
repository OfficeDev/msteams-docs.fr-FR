---
title: Événements de conversation
author: WashingtonKayaker
description: Comment travailler avec des événements de conversation à partir de votre bot Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: af1724620ede44f8d0f7739e265ef1ebd1e3afd8
ms.sourcegitcommit: 0e252159f53ff9b4452e0574b759bfe73cbf6c84
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2021
ms.locfileid: "51762031"
---
# <a name="conversation-events-in-your-teams-bot"></a><span data-ttu-id="cc73d-103">Événements de conversation dans votre robot Teams</span><span class="sxs-lookup"><span data-stu-id="cc73d-103">Conversation events in your Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="cc73d-104">Lorsque vous construisez vos bots de conversation pour Microsoft Teams, vous pouvez utiliser des événements de conversation.</span><span class="sxs-lookup"><span data-stu-id="cc73d-104">When building your conversational bots for Microsoft Teams, you can work with conversation events.</span></span> <span data-ttu-id="cc73d-105">Teams envoie des notifications à votre bot pour les événements de conversation qui se produisent dans les étendues où votre bot est actif.</span><span class="sxs-lookup"><span data-stu-id="cc73d-105">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="cc73d-106">Vous pouvez capturer ces événements dans votre code et prendre les mesures suivantes :</span><span class="sxs-lookup"><span data-stu-id="cc73d-106">You can capture these events in your code and take the following actions:</span></span>

* <span data-ttu-id="cc73d-107">Déclencher un message de bienvenue lorsque votre bot est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="cc73d-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="cc73d-108">Déclencher un message de bienvenue lorsqu'un nouveau membre d'équipe est ajouté ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-108">Trigger a welcome message when a new team member is added or removed.</span></span>
* <span data-ttu-id="cc73d-109">Déclencher une notification lorsqu'un canal est créé, renommé ou supprimé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-109">Trigger a notification when a channel is created, renamed, or deleted.</span></span>
* <span data-ttu-id="cc73d-110">Lorsqu'un message bot est aimé par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc73d-110">When a bot message is liked by a user.</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="cc73d-111">Événements de mise à jour de conversation</span><span class="sxs-lookup"><span data-stu-id="cc73d-111">Conversation update events</span></span>

<span data-ttu-id="cc73d-112">Vous pouvez utiliser les événements de mise à jour de conversation pour fournir de meilleures notifications et des actions de bot plus efficaces.</span><span class="sxs-lookup"><span data-stu-id="cc73d-112">You can use conversation update events to provide better notifications and more effective bot actions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="cc73d-113">Vous pouvez ajouter de nouveaux événements à tout moment et votre bot commence à les recevoir.</span><span class="sxs-lookup"><span data-stu-id="cc73d-113">You can add new events any time and your bot begins to receive them.</span></span>
> * <span data-ttu-id="cc73d-114">Vous devez concevoir votre bot pour recevoir des événements inattendus.</span><span class="sxs-lookup"><span data-stu-id="cc73d-114">You must design your bot to receive unexpected events.</span></span>
> * <span data-ttu-id="cc73d-115">Si vous utilisez le SDK Bot Framework, votre bot répond automatiquement à tous les événements que vous choisissez de `200 - OK` ne pas gérer.</span><span class="sxs-lookup"><span data-stu-id="cc73d-115">If you are using the Bot Framework SDK, your bot automatically responds with a `200 - OK` to any events you choose not to handle.</span></span>

<span data-ttu-id="cc73d-116">Un bot reçoit un `conversationUpdate` événement dans l'un des cas suivants :</span><span class="sxs-lookup"><span data-stu-id="cc73d-116">A bot receives a `conversationUpdate` event in either of the following cases:</span></span>

* <span data-ttu-id="cc73d-117">Lorsque le bot a été ajouté à une conversation.</span><span class="sxs-lookup"><span data-stu-id="cc73d-117">When bot has been added to a conversation.</span></span>
* <span data-ttu-id="cc73d-118">D'autres membres sont ajoutés à une conversation ou supprimés d'une conversation.</span><span class="sxs-lookup"><span data-stu-id="cc73d-118">Other members are added to or removed from a conversation.</span></span>
* <span data-ttu-id="cc73d-119">Les métadonnées de conversation ont changé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-119">Conversation metadata has changed.</span></span>

<span data-ttu-id="cc73d-120">L’événement `conversationUpdate` est envoyé à votre robot lorsqu’il reçoit des informations sur les mises à jour d’appartenance pour les équipes dans lesquelles il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="cc73d-120">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="cc73d-121">Il reçoit également une mise à jour lorsqu'elle a été ajoutée pour la première fois pour des conversations personnelles.</span><span class="sxs-lookup"><span data-stu-id="cc73d-121">It also receives an update when it has been added for the first time for personal conversations.</span></span>

<span data-ttu-id="cc73d-122">Le tableau suivant présente la liste des événements de mise à jour de conversation Teams avec plus de détails :</span><span class="sxs-lookup"><span data-stu-id="cc73d-122">The following table shows a list of Teams conversation update events with more details:</span></span>

| <span data-ttu-id="cc73d-123">Action prise</span><span class="sxs-lookup"><span data-stu-id="cc73d-123">Action taken</span></span>        | <span data-ttu-id="cc73d-124">EventType</span><span class="sxs-lookup"><span data-stu-id="cc73d-124">EventType</span></span>         | <span data-ttu-id="cc73d-125">Méthode appelée</span><span class="sxs-lookup"><span data-stu-id="cc73d-125">Method called</span></span>              | <span data-ttu-id="cc73d-126">Description</span><span class="sxs-lookup"><span data-stu-id="cc73d-126">Description</span></span>                | <span data-ttu-id="cc73d-127">Portée</span><span class="sxs-lookup"><span data-stu-id="cc73d-127">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="cc73d-128">Canal créé</span><span class="sxs-lookup"><span data-stu-id="cc73d-128">Channel created</span></span>     | <span data-ttu-id="cc73d-129">channelCreated</span><span class="sxs-lookup"><span data-stu-id="cc73d-129">channelCreated</span></span>    | <span data-ttu-id="cc73d-130">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-130">OnTeamsChannelCreatedAsync</span></span> | <span data-ttu-id="cc73d-131">[Un canal est créé.](#channel-created)</span><span class="sxs-lookup"><span data-stu-id="cc73d-131">[A channel is created](#channel-created).</span></span> | <span data-ttu-id="cc73d-132">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-132">Team</span></span> |
| <span data-ttu-id="cc73d-133">Canal renommé</span><span class="sxs-lookup"><span data-stu-id="cc73d-133">Channel renamed</span></span>     | <span data-ttu-id="cc73d-134">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="cc73d-134">channelRenamed</span></span>    | <span data-ttu-id="cc73d-135">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-135">OnTeamsChannelRenamedAsync</span></span> | <span data-ttu-id="cc73d-136">[Un canal est renommé](#channel-renamed).</span><span class="sxs-lookup"><span data-stu-id="cc73d-136">[A channel is renamed](#channel-renamed).</span></span> | <span data-ttu-id="cc73d-137">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-137">Team</span></span> |
| <span data-ttu-id="cc73d-138">Canal supprimé</span><span class="sxs-lookup"><span data-stu-id="cc73d-138">Channel deleted</span></span>     | <span data-ttu-id="cc73d-139">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="cc73d-139">channelDeleted</span></span>    | <span data-ttu-id="cc73d-140">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-140">OnTeamsChannelDeletedAsync</span></span> | <span data-ttu-id="cc73d-141">[Un canal est supprimé.](#channel-deleted)</span><span class="sxs-lookup"><span data-stu-id="cc73d-141">[A channel is deleted](#channel-deleted).</span></span> | <span data-ttu-id="cc73d-142">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-142">Team</span></span> |
| <span data-ttu-id="cc73d-143">Canal restauré</span><span class="sxs-lookup"><span data-stu-id="cc73d-143">Channel restored</span></span>    | <span data-ttu-id="cc73d-144">channelRestored</span><span class="sxs-lookup"><span data-stu-id="cc73d-144">channelRestored</span></span>    | <span data-ttu-id="cc73d-145">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-145">OnTeamsChannelRestoredAsync</span></span> | <span data-ttu-id="cc73d-146">[Un canal est restauré.](#channel-deleted)</span><span class="sxs-lookup"><span data-stu-id="cc73d-146">[A channel is restored](#channel-deleted).</span></span> | <span data-ttu-id="cc73d-147">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-147">Team</span></span> |
| <span data-ttu-id="cc73d-148">Membres ajoutés</span><span class="sxs-lookup"><span data-stu-id="cc73d-148">Members added</span></span>   | <span data-ttu-id="cc73d-149">membersAdded</span><span class="sxs-lookup"><span data-stu-id="cc73d-149">membersAdded</span></span>   | <span data-ttu-id="cc73d-150">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-150">OnTeamsMembersAddedAsync</span></span>   | <span data-ttu-id="cc73d-151">[Un membre est ajouté.](#team-members-added)</span><span class="sxs-lookup"><span data-stu-id="cc73d-151">[A member is added](#team-members-added).</span></span> | <span data-ttu-id="cc73d-152">Tous</span><span class="sxs-lookup"><span data-stu-id="cc73d-152">All</span></span> |
| <span data-ttu-id="cc73d-153">Membres supprimés</span><span class="sxs-lookup"><span data-stu-id="cc73d-153">Members removed</span></span> | <span data-ttu-id="cc73d-154">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="cc73d-154">membersRemoved</span></span> | <span data-ttu-id="cc73d-155">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-155">OnTeamsMembersRemovedAsync</span></span> | <span data-ttu-id="cc73d-156">[Un membre est supprimé.](#team-members-removed)</span><span class="sxs-lookup"><span data-stu-id="cc73d-156">[A member is removed](#team-members-removed).</span></span> | <span data-ttu-id="cc73d-157">groupChat et équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-157">groupChat and team</span></span> |
| <span data-ttu-id="cc73d-158">Équipe renommée</span><span class="sxs-lookup"><span data-stu-id="cc73d-158">Team renamed</span></span>        | <span data-ttu-id="cc73d-159">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="cc73d-159">teamRenamed</span></span>       | <span data-ttu-id="cc73d-160">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-160">OnTeamsTeamRenamedAsync</span></span>    | <span data-ttu-id="cc73d-161">[Une équipe est renommée.](#team-renamed)</span><span class="sxs-lookup"><span data-stu-id="cc73d-161">[A team is renamed](#team-renamed).</span></span>       | <span data-ttu-id="cc73d-162">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-162">Team</span></span> |
| <span data-ttu-id="cc73d-163">Équipe supprimée</span><span class="sxs-lookup"><span data-stu-id="cc73d-163">Team deleted</span></span>        | <span data-ttu-id="cc73d-164">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="cc73d-164">teamDeleted</span></span>       | <span data-ttu-id="cc73d-165">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-165">OnTeamsTeamDeletedAsync</span></span>    | <span data-ttu-id="cc73d-166">[Une équipe est supprimée.](#team-deleted)</span><span class="sxs-lookup"><span data-stu-id="cc73d-166">[A team is deleted](#team-deleted).</span></span>       | <span data-ttu-id="cc73d-167">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-167">Team</span></span> |
| <span data-ttu-id="cc73d-168">Équipe archivée</span><span class="sxs-lookup"><span data-stu-id="cc73d-168">Team archived</span></span>        | <span data-ttu-id="cc73d-169">teamArchived</span><span class="sxs-lookup"><span data-stu-id="cc73d-169">teamArchived</span></span>       | <span data-ttu-id="cc73d-170">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-170">OnTeamsTeamArchivedAsync</span></span>    | <span data-ttu-id="cc73d-171">[Une équipe est archivée.](#team-archived)</span><span class="sxs-lookup"><span data-stu-id="cc73d-171">[A team is archived](#team-archived).</span></span>       | <span data-ttu-id="cc73d-172">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-172">Team</span></span> |
| <span data-ttu-id="cc73d-173">Équipe nonarchived</span><span class="sxs-lookup"><span data-stu-id="cc73d-173">Team unarchived</span></span>        | <span data-ttu-id="cc73d-174">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="cc73d-174">teamUnarchived</span></span>       | <span data-ttu-id="cc73d-175">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-175">OnTeamsTeamUnarchivedAsync</span></span>    | <span data-ttu-id="cc73d-176">[Une équipe n'est pasarchive.](#team-unarchived)</span><span class="sxs-lookup"><span data-stu-id="cc73d-176">[A team is unarchived](#team-unarchived).</span></span>       | <span data-ttu-id="cc73d-177">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-177">Team</span></span> |
| <span data-ttu-id="cc73d-178">Équipe restaurée</span><span class="sxs-lookup"><span data-stu-id="cc73d-178">Team restored</span></span>        | <span data-ttu-id="cc73d-179">teamRestored</span><span class="sxs-lookup"><span data-stu-id="cc73d-179">teamRestored</span></span>      | <span data-ttu-id="cc73d-180">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="cc73d-180">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="cc73d-181">Une équipe est restaurée</span><span class="sxs-lookup"><span data-stu-id="cc73d-181">A team is restored</span></span>](#team-restored)       | <span data-ttu-id="cc73d-182">Équipe</span><span class="sxs-lookup"><span data-stu-id="cc73d-182">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="cc73d-183">Canal créé</span><span class="sxs-lookup"><span data-stu-id="cc73d-183">Channel created</span></span>

<span data-ttu-id="cc73d-184">L'événement créé par le canal est envoyé à votre bot chaque fois qu'un nouveau canal est créé dans une équipe où votre bot est installé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-184">The channel created event is sent to your bot whenever a new channel is created in a team where your bot is installed.</span></span>

<span data-ttu-id="cc73d-185">Le code suivant montre un exemple d'événement de canal créé :</span><span class="sxs-lookup"><span data-stu-id="cc73d-185">The following code shows an example of channel created event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-186">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-186">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-187">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-187">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-188">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-189">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-189">Python</span></span>](#tab/python)

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

### <a name="channel-renamed"></a><span data-ttu-id="cc73d-190">Canal renommé</span><span class="sxs-lookup"><span data-stu-id="cc73d-190">Channel renamed</span></span>

<span data-ttu-id="cc73d-191">L'événement renommé de canal est envoyé à votre bot chaque fois qu'un canal est renommé dans une équipe où votre bot est installé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-191">The channel renamed event is sent to your bot whenever a channel is renamed in a team where your bot is installed.</span></span>

<span data-ttu-id="cc73d-192">Le code suivant montre un exemple d'événement de changement de nom de canal :</span><span class="sxs-lookup"><span data-stu-id="cc73d-192">The following code shows an example of channel renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-193">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-194">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-195">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-195">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-196">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-196">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="cc73d-197">Canal supprimé</span><span class="sxs-lookup"><span data-stu-id="cc73d-197">Channel deleted</span></span>

<span data-ttu-id="cc73d-198">L'événement de canal supprimé est envoyé à votre bot chaque fois qu'un canal est supprimé dans une équipe où votre bot est installé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-198">The channel deleted event is sent to your bot whenever a channel is deleted in a team where your bot is installed.</span></span>

<span data-ttu-id="cc73d-199">Le code suivant montre un exemple d'événement de suppression de canal :</span><span class="sxs-lookup"><span data-stu-id="cc73d-199">The following code shows an example of channel deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-200">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-200">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-201">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-201">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-202">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-202">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-203">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-203">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="cc73d-204">Canal restauré</span><span class="sxs-lookup"><span data-stu-id="cc73d-204">Channel restored</span></span>

<span data-ttu-id="cc73d-205">L'événement de restauration de canal est envoyé à votre bot chaque fois qu'un canal précédemment supprimé est restauré dans une équipe où votre bot est déjà installé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-205">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team where your bot is already installed.</span></span>

<span data-ttu-id="cc73d-206">Le code suivant montre un exemple d'événement de restauration de canal :</span><span class="sxs-lookup"><span data-stu-id="cc73d-206">The following code shows an example of channel restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-207">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-207">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-208">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-208">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-209">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-209">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-210">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-210">Python</span></span>](#tab/python)

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

### <a name="team-members-added"></a><span data-ttu-id="cc73d-211">Membres d'équipe ajoutés</span><span class="sxs-lookup"><span data-stu-id="cc73d-211">Team members added</span></span>

<span data-ttu-id="cc73d-212">L'événement est envoyé à votre bot la première fois qu'il est `teamMemberAdded` ajouté à une conversation.</span><span class="sxs-lookup"><span data-stu-id="cc73d-212">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation.</span></span> <span data-ttu-id="cc73d-213">L'événement est envoyé à votre bot chaque fois qu'un nouvel utilisateur est ajouté à une conversation d'équipe ou de groupe où votre bot est installé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-213">The event is sent to your bot every time a new user is added to a team or group chat where your bot is installed.</span></span> <span data-ttu-id="cc73d-214">Les informations utilisateur qui sont des ID sont uniques pour votre bot et peuvent être mises en cache pour une utilisation ultérieure par votre service, telles que l'envoi d'un message à un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="cc73d-214">The user information that is ID is unique for your bot and can be cached for future use by your service, such as sending a message to a specific user.</span></span>

<span data-ttu-id="cc73d-215">Le code suivant montre un exemple d'événement ajouté aux membres de l'équipe :</span><span class="sxs-lookup"><span data-stu-id="cc73d-215">The following code shows an example of team members added event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-216">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-216">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="cc73d-217">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-217">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-218">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-218">JSON</span></span>](#tab/json)

<span data-ttu-id="cc73d-219">Il s'agit du message que votre bot reçoit lorsque le bot est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="cc73d-219">This is the message your bot receives when the bot is added to a team.</span></span>

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

<span data-ttu-id="cc73d-220">Il s'agit du message que votre bot reçoit lorsque le bot est ajouté à une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="cc73d-220">This is the message your bot receives when the bot is added to a one-to-one chat.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="cc73d-221">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-221">Python</span></span>](#tab/python)

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

* * *

### <a name="team-members-removed"></a><span data-ttu-id="cc73d-222">Membres d'équipe supprimés</span><span class="sxs-lookup"><span data-stu-id="cc73d-222">Team members removed</span></span>

<span data-ttu-id="cc73d-223">`teamMemberRemoved`L'événement est envoyé à votre bot s'il est supprimé d'une équipe.</span><span class="sxs-lookup"><span data-stu-id="cc73d-223">The `teamMemberRemoved` event is sent to your bot if it is removed from a team.</span></span> <span data-ttu-id="cc73d-224">L'événement est envoyé à votre bot chaque fois qu'un utilisateur est supprimé d'une équipe dont il est membre.</span><span class="sxs-lookup"><span data-stu-id="cc73d-224">The event is sent to your bot every time any user is removed from a team where your bot is a member.</span></span> <span data-ttu-id="cc73d-225">Pour déterminer si le nouveau membre supprimé était le bot lui-même ou un utilisateur, vérifiez `Activity` l'objet du `turnContext` .</span><span class="sxs-lookup"><span data-stu-id="cc73d-225">To determine if the new member removed was the bot itself or a user, check the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="cc73d-226">Si le champ de l'objet est identique au champ de l'objet, le membre supprimé est le bot, sinon il `Id` `MembersRemoved` `Id` s'agit `Recipient` d'un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cc73d-226">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, else it is a user.</span></span> <span data-ttu-id="cc73d-227">Le bot est `Id` généralement `28:<MicrosoftAppId>` .</span><span class="sxs-lookup"><span data-stu-id="cc73d-227">The bot's `Id` generally is `28:<MicrosoftAppId>`.</span></span>

> [!NOTE]
> <span data-ttu-id="cc73d-228">Lorsqu'un utilisateur est définitivement supprimé d'un client, `membersRemoved conversationUpdate` l'événement est déclenché.</span><span class="sxs-lookup"><span data-stu-id="cc73d-228">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

<span data-ttu-id="cc73d-229">Le code suivant montre un exemple d'événement supprimé des membres de l'équipe :</span><span class="sxs-lookup"><span data-stu-id="cc73d-229">The following code shows an example of team members removed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-230">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-230">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="cc73d-231">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-231">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-232">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-232">JSON</span></span>](#tab/json)

<span data-ttu-id="cc73d-233">L'objet de l'exemple de charge utile suivant est basé sur l'ajout d'un membre à une équipe plutôt qu'à une conversation de groupe ou sur le début d'une nouvelle `channelData` conversation un-à-un :</span><span class="sxs-lookup"><span data-stu-id="cc73d-233">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="cc73d-234">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-234">Python</span></span>](#tab/python)

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

### <a name="team-renamed"></a><span data-ttu-id="cc73d-235">Équipe renommée</span><span class="sxs-lookup"><span data-stu-id="cc73d-235">Team renamed</span></span>

<span data-ttu-id="cc73d-236">Votre bot est averti lorsque l'équipe dans qui il se trouve a été renommé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-236">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="cc73d-237">Il reçoit un `conversationUpdate` événement avec `eventType.teamRenamed` dans `channelData` l'objet.</span><span class="sxs-lookup"><span data-stu-id="cc73d-237">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

<span data-ttu-id="cc73d-238">Le code suivant montre un exemple d'événement renommé d'équipe :</span><span class="sxs-lookup"><span data-stu-id="cc73d-238">The following code shows an example of team renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-239">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-239">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-240">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-240">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-241">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-242">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="cc73d-243">Équipe supprimée</span><span class="sxs-lookup"><span data-stu-id="cc73d-243">Team deleted</span></span>

<span data-ttu-id="cc73d-244">Votre bot est averti lorsque l'équipe dans qui elle se trouve a été supprimée.</span><span class="sxs-lookup"><span data-stu-id="cc73d-244">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="cc73d-245">Il reçoit un `conversationUpdate` événement avec `eventType.teamDeleted` dans `channelData` l'objet.</span><span class="sxs-lookup"><span data-stu-id="cc73d-245">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

<span data-ttu-id="cc73d-246">Le code suivant illustre un exemple d'événement supprimé par l'équipe :</span><span class="sxs-lookup"><span data-stu-id="cc73d-246">The following code shows an example of team deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-247">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-247">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-248">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-248">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-249">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-249">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-250">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="cc73d-251">Équipe restaurée</span><span class="sxs-lookup"><span data-stu-id="cc73d-251">Team restored</span></span>

<span data-ttu-id="cc73d-252">Le bot reçoit une notification lorsqu'une équipe est restaurée après avoir été supprimée.</span><span class="sxs-lookup"><span data-stu-id="cc73d-252">The bot receives a notification when a team is restored after being deleted.</span></span> <span data-ttu-id="cc73d-253">Il reçoit un `conversationUpdate` événement avec `eventType.teamrestored` dans `channelData` l'objet.</span><span class="sxs-lookup"><span data-stu-id="cc73d-253">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

<span data-ttu-id="cc73d-254">Le code suivant illustre un exemple d'événement restauré par l'équipe :</span><span class="sxs-lookup"><span data-stu-id="cc73d-254">The following code shows an example of team restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-255">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-255">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-256">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-256">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-257">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-257">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-258">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-258">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="cc73d-259">Équipe archivée</span><span class="sxs-lookup"><span data-stu-id="cc73d-259">Team archived</span></span>

<span data-ttu-id="cc73d-260">Le bot reçoit une notification lorsque l'équipe dans qui il est installé est archivée.</span><span class="sxs-lookup"><span data-stu-id="cc73d-260">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="cc73d-261">Il reçoit un `conversationUpdate` événement avec `eventType.teamarchived` dans `channelData` l'objet.</span><span class="sxs-lookup"><span data-stu-id="cc73d-261">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

<span data-ttu-id="cc73d-262">Le code suivant montre un exemple d'événement d'équipe archivé :</span><span class="sxs-lookup"><span data-stu-id="cc73d-262">The following code shows an example of team archived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-263">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-263">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-264">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-264">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-265">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-265">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-266">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-266">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="cc73d-267">Équipe nonarchived</span><span class="sxs-lookup"><span data-stu-id="cc73d-267">Team unarchived</span></span>

<span data-ttu-id="cc73d-268">Le bot reçoit une notification lorsque l'équipe dans qui il est installé n'est pasarchived.</span><span class="sxs-lookup"><span data-stu-id="cc73d-268">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="cc73d-269">Il reçoit un `conversationUpdate` événement avec `eventType.teamUnarchived` dans `channelData` l'objet.</span><span class="sxs-lookup"><span data-stu-id="cc73d-269">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

<span data-ttu-id="cc73d-270">Le code suivant montre un exemple d'événement d'équipe nonarchif :</span><span class="sxs-lookup"><span data-stu-id="cc73d-270">The following code shows an example of team unarchived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-271">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-271">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="cc73d-272">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-272">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-273">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-273">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-274">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-274">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

<span data-ttu-id="cc73d-275">Maintenant que vous avez travaillé avec les événements de mise à jour de conversation, vous pouvez comprendre les événements de réaction de message qui se produisent pour différentes réactions à un message.</span><span class="sxs-lookup"><span data-stu-id="cc73d-275">Now that you have worked with the conversation update events, you can understand the message reaction events that occur for different reactions to a message.</span></span>

## <a name="message-reaction-events"></a><span data-ttu-id="cc73d-276">Événements de réaction aux messages</span><span class="sxs-lookup"><span data-stu-id="cc73d-276">Message reaction events</span></span>

<span data-ttu-id="cc73d-277">L'événement est envoyé lorsqu'un utilisateur ajoute ou supprime des réactions à un message envoyé `messageReaction` par votre bot.</span><span class="sxs-lookup"><span data-stu-id="cc73d-277">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="cc73d-278">Contient l'ID du message et le type de réaction au `replyToId` `Type` format texte.</span><span class="sxs-lookup"><span data-stu-id="cc73d-278">The `replyToId` contains the ID of the message, and the `Type` is the type of reaction in text format.</span></span> <span data-ttu-id="cc73d-279">Les types de réactions incluent notamment la femme, le cœur, l'homme, le genre, la peine et la surprise.</span><span class="sxs-lookup"><span data-stu-id="cc73d-279">The types of reactions include angry, heart, laugh, like, sad, and surprised.</span></span> <span data-ttu-id="cc73d-280">Cet événement ne contient pas le contenu du message d'origine.</span><span class="sxs-lookup"><span data-stu-id="cc73d-280">This event does not contain the contents of the original message.</span></span> <span data-ttu-id="cc73d-281">Si le traitement des réactions à vos messages est important pour votre bot, vous devez stocker les messages lorsque vous les envoyez.</span><span class="sxs-lookup"><span data-stu-id="cc73d-281">If processing reactions to your messages is important for your bot, you must store the messages when you send them.</span></span> <span data-ttu-id="cc73d-282">Le tableau suivant fournit plus d'informations sur le type d'événement et les objets de charge utile :</span><span class="sxs-lookup"><span data-stu-id="cc73d-282">The following table provides more information about the event type and payload objects:</span></span>

| <span data-ttu-id="cc73d-283">EventType</span><span class="sxs-lookup"><span data-stu-id="cc73d-283">EventType</span></span>       | <span data-ttu-id="cc73d-284">Objet Payload</span><span class="sxs-lookup"><span data-stu-id="cc73d-284">Payload object</span></span>   | <span data-ttu-id="cc73d-285">Description</span><span class="sxs-lookup"><span data-stu-id="cc73d-285">Description</span></span>                                                             | <span data-ttu-id="cc73d-286">Portée</span><span class="sxs-lookup"><span data-stu-id="cc73d-286">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="cc73d-287">messageReaction</span><span class="sxs-lookup"><span data-stu-id="cc73d-287">messageReaction</span></span> | <span data-ttu-id="cc73d-288">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="cc73d-288">reactionsAdded</span></span>   | <span data-ttu-id="cc73d-289">[Réactions ajoutées au message du bot.](#reactions-added-to-bot-message)</span><span class="sxs-lookup"><span data-stu-id="cc73d-289">[Reactions added to bot message](#reactions-added-to-bot-message).</span></span>           | <span data-ttu-id="cc73d-290">Tous</span><span class="sxs-lookup"><span data-stu-id="cc73d-290">All</span></span>   |
| <span data-ttu-id="cc73d-291">messageReaction</span><span class="sxs-lookup"><span data-stu-id="cc73d-291">messageReaction</span></span> | <span data-ttu-id="cc73d-292">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="cc73d-292">reactionsRemoved</span></span> | <span data-ttu-id="cc73d-293">[Réactions supprimées du message du bot.](#reactions-removed-from-bot-message)</span><span class="sxs-lookup"><span data-stu-id="cc73d-293">[Reactions removed from bot message](#reactions-removed-from-bot-message).</span></span> | <span data-ttu-id="cc73d-294">Tous</span><span class="sxs-lookup"><span data-stu-id="cc73d-294">All</span></span> |

### <a name="reactions-added-to-bot-message"></a><span data-ttu-id="cc73d-295">Réactions ajoutées au message du bot</span><span class="sxs-lookup"><span data-stu-id="cc73d-295">Reactions added to bot message</span></span>

<span data-ttu-id="cc73d-296">Le code suivant montre un exemple de réactions à un message de bot :</span><span class="sxs-lookup"><span data-stu-id="cc73d-296">The following code shows an example of reactions to a bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-297">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-297">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="cc73d-298">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-298">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-299">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-299">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-300">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-300">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="cc73d-301">Réactions supprimées du message du bot</span><span class="sxs-lookup"><span data-stu-id="cc73d-301">Reactions removed from bot message</span></span>

<span data-ttu-id="cc73d-302">Le code suivant montre un exemple de réactions supprimées du message du bot :</span><span class="sxs-lookup"><span data-stu-id="cc73d-302">The following code shows an example of reactions removed from bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="cc73d-303">C#</span><span class="sxs-lookup"><span data-stu-id="cc73d-303">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="cc73d-304">TypeScript</span><span class="sxs-lookup"><span data-stu-id="cc73d-304">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="cc73d-305">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-305">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="cc73d-306">Python</span><span class="sxs-lookup"><span data-stu-id="cc73d-306">Python</span></span>](#tab/python)

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

## <a name="installation-update-event"></a><span data-ttu-id="cc73d-307">Événement de mise à jour d'installation</span><span class="sxs-lookup"><span data-stu-id="cc73d-307">Installation update event</span></span>

<span data-ttu-id="cc73d-308">Le bot reçoit un `installationUpdate` événement lorsque vous installez un bot sur un thread de conversation.</span><span class="sxs-lookup"><span data-stu-id="cc73d-308">The bot receives an `installationUpdate` event when you install a bot to a conversation thread.</span></span> <span data-ttu-id="cc73d-309">La désinstallation du bot du thread déclenche également l'événement.</span><span class="sxs-lookup"><span data-stu-id="cc73d-309">Uninstallation of the bot from the thread also triggers the event.</span></span> <span data-ttu-id="cc73d-310">Lors de l'installation d'un bot, le champ **d'action** dans l'événement est définie pour ajouter *,* et lorsque le bot est désinstallé, le champ **d'action** est définie pour *supprimer*.</span><span class="sxs-lookup"><span data-stu-id="cc73d-310">On installing a bot, the **action** field in the event is set to *add*, and when the bot is uninstalled the **action** field is set to *remove*.</span></span>
 
> [!NOTE]
> <span data-ttu-id="cc73d-311">Lorsque vous mettre à niveau une application, puis ajoutez ou supprimez un bot, l'action déclenche également `installationUpdate` l'événement.</span><span class="sxs-lookup"><span data-stu-id="cc73d-311">When you upgrade an application, and then add or remove a bot, the action also triggers the `installationUpdate` event.</span></span> <span data-ttu-id="cc73d-312">Le **champ d'action** est définie sur *add-upgrade* si vous ajoutez un bot ou *remove-upgrade* si vous supprimez un bot.</span><span class="sxs-lookup"><span data-stu-id="cc73d-312">The **action** field is set to *add-upgrade* if you add a bot or *remove-upgrade* if you remove a bot.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="cc73d-313">Les événements de mise à jour d'installation sont en version préliminaire pour les développeurs aujourd'hui et seront généralement disponibles en mars 2021.</span><span class="sxs-lookup"><span data-stu-id="cc73d-313">Installation update events are in developer preview today and will be Generally Available (GA) in March 2021.</span></span> <span data-ttu-id="cc73d-314">Pour afficher les événements de mise à jour d'installation, vous pouvez déplacer votre client Teams vers la prévisualisation publique pour les développeurs et ajouter votre application à titre personnel, à une équipe ou à une conversation.</span><span class="sxs-lookup"><span data-stu-id="cc73d-314">To see the installation update events, you can move your Teams client to public developer preview, and add your app personally or to a team or a chat.</span></span>

### <a name="install-update-event"></a><span data-ttu-id="cc73d-315">Installer l'événement de mise à jour</span><span class="sxs-lookup"><span data-stu-id="cc73d-315">Install update event</span></span>
<span data-ttu-id="cc73d-316">Utilisez `installationUpdate` l'événement pour envoyer un message d'introduction à partir de votre bot lors de l'installation.</span><span class="sxs-lookup"><span data-stu-id="cc73d-316">Use the `installationUpdate` event to send an introductory message from your bot on installation.</span></span> <span data-ttu-id="cc73d-317">Cet événement vous aide à répondre à vos exigences de confidentialité et de rétention des données.</span><span class="sxs-lookup"><span data-stu-id="cc73d-317">This event helps you to meet your privacy and data retention requirements.</span></span> <span data-ttu-id="cc73d-318">Vous pouvez également nettoyer et supprimer des données utilisateur ou thread lorsque le bot est désinstallé.</span><span class="sxs-lookup"><span data-stu-id="cc73d-318">You can also clean up and delete user or thread data when the bot is uninstalled.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="cc73d-319">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="cc73d-319">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task
OnInstallationUpdateActivityAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken) {
var activity = turnContext.Activity; if
(string.Equals(activity.Action, "Add",
StringComparison.InvariantCultureIgnoreCase)) {
// TO:DO Installation workflow }
else
{ // TO:DO Uninstallation workflow
} return; }
```

<span data-ttu-id="cc73d-320">Vous pouvez également utiliser un  handler dédié pour ajouter ou supprimer des *scénarios* en tant que méthode alternative pour capturer un événement.</span><span class="sxs-lookup"><span data-stu-id="cc73d-320">You can also use a dedicated handler for *add* or *remove* scenarios as an alternative method to capture an event.</span></span>

```csharp
protected override async Task
OnInstallationUpdateAddAsync(ITurnContext<IInstallationUpdateActivity>
turnContext, CancellationToken cancellationToken) {
// TO:DO Installation workflow return;
}
```

# <a name="json"></a>[<span data-ttu-id="cc73d-321">JSON</span><span class="sxs-lookup"><span data-stu-id="cc73d-321">JSON</span></span>](#tab/json)

```json
{ 
  "action": "add", 
  "type": "installationUpdate", 
  "timestamp": "2020-10-20T22:08:07.869Z", 
  "id": "f:3033745319439849398", 
  "channelId": "msteams", 
  "serviceUrl": "https://smba.trafficmanager.net/amer/", 
  "from": { 
    "id": "sample id", 
    "aadObjectId": "sample AAD Object ID" 
  },
  "conversation": { 
    "isGroup": true, 
    "conversationType": "channel", 
    "tenantId": "sample tenant ID", 
    "id": "sample conversation Id@thread.skype" 
  }, 

  "recipient": { 
    "id": "sample reciepent bot ID", 
    "name": "bot name" 
  }, 
  "entities": [ 
    { 
      "locale": "en", 
      "platform": "Windows", 
      "type": "clientInfo" 
    } 
  ], 
  "channelData": { 
    "settings": { 
      "selectedChannel": { 
        "id": "sample channel ID@thread.skype" 
      } 
    }, 
    "channel": { 
      "id": "sample channel ID" 
    }, 
    "team": { 
      "id": "sample team ID" 
    }, 
    "tenant": { 
      "id": "sample tenant ID" 
    }, 
    "source": { 
      "name": "message" 
    } 
  }, 
  "locale": "en" 
}
```
* * *

## <a name="code-sample"></a><span data-ttu-id="cc73d-322">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="cc73d-322">Code sample</span></span>

| <span data-ttu-id="cc73d-323">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="cc73d-323">**Sample name**</span></span> | <span data-ttu-id="cc73d-324">**Description**</span><span class="sxs-lookup"><span data-stu-id="cc73d-324">**Description**</span></span> | <span data-ttu-id="cc73d-325">**.NET**</span><span class="sxs-lookup"><span data-stu-id="cc73d-325">**.NET**</span></span> |
|-----------------|-----------------|---------|
|<span data-ttu-id="cc73d-326">Événements de conversation des bots Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="cc73d-326">Microsoft Teams bots conversation events</span></span> | <span data-ttu-id="cc73d-327">Exemple d'événements de bot.</span><span class="sxs-lookup"><span data-stu-id="cc73d-327">Sample for bot events.</span></span> | [<span data-ttu-id="cc73d-328">View</span><span class="sxs-lookup"><span data-stu-id="cc73d-328">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="cc73d-329">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="cc73d-329">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cc73d-330">Envoyer des messages proactifs</span><span class="sxs-lookup"><span data-stu-id="cc73d-330">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
