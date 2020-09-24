---
title: Obtenir le contexte spécifique de l’équipe pour votre robot
author: clearab
description: Comment obtenir le contexte spécifique de l’équipe Microsoft de votre robot, y compris la liste de conversation, les détails et la liste des canaux.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 55f93a914cdb0f92885ff535424cd823072184aa
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237791"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="5fdc6-103">Obtenir le contexte spécifique de l’équipe pour votre robot</span><span class="sxs-lookup"><span data-stu-id="5fdc6-103">Get Team's specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="5fdc6-104">Un bot peut accéder à des données de contexte supplémentaires sur une équipe ou une conversation dans laquelle il est installé.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-104">A bot can access additional context data about a team or chat it is installed in.</span></span> <span data-ttu-id="5fdc6-105">Ces informations peuvent être utilisées pour enrichir les fonctionnalités du robot et fournir une expérience plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetching-the-roster-or-user-profile"></a><span data-ttu-id="5fdc6-106">Extraction de la liste ou du profil utilisateur</span><span class="sxs-lookup"><span data-stu-id="5fdc6-106">Fetching the roster or user profile</span></span>

<span data-ttu-id="5fdc6-107">Votre bot peut interroger la liste des membres et leurs profils de base, y compris les ID utilisateur teams et les informations Azure Active Directory (Azure AD), telles que nom et objectId.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-107">Your bot can query for the list of members and their basic profiles, including Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="5fdc6-108">Vous pouvez utiliser ces informations pour corréler les identités des utilisateurs, par exemple, pour vérifier si un utilisateur s’est connecté à un onglet par le biais des informations d’identification Azure AD, est membre de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-108">You can use this information to correlate user identities, e.g., to check whether a user, logged into a tab through Azure AD credentials, is a member of the team.</span></span> <span data-ttu-id="5fdc6-109">L’exemple de code ci-dessous utilise le point de terminaison paginé pour extraire la liste.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-109">The sample code below uses the paged endpoint for retrieving the roster.</span></span> <span data-ttu-id="5fdc6-110">Bien que vous pouvez toujours utiliser la version non paginée, elle n’est pas fiable dans les grandes équipes et ne doit pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-110">Although you may still use the non-paged version, it will be unreliable in large teams and should not be used.</span></span> <span data-ttu-id="5fdc6-111">Pour plus d’informations, consultez [cet article](~/resources/team-chat-member-api-changes.md) .</span><span class="sxs-lookup"><span data-stu-id="5fdc6-111">See [this article](~/resources/team-chat-member-api-changes.md) for additional information.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5fdc6-112">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5fdc6-112">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var members = new List<TeamsChannelAccount>();
        string continuationToken = null;

        do
        {
            var currentPage = await TeamsInfo.GetPagedMembersAsync(turnContext, 100, continuationToken, cancellationToken);
            continuationToken = currentPage.ContinuationToken;
            members.AddRange(currentPage.Members);
         }
         while (continuationToken != null);
     }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5fdc6-113">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5fdc6-113">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            var continuationToken;
            var members = [];

            do {
                var pagedMembers = await TeamsInfo.getPagedMembers(context, 100, continuationToken);
                continuationToken = pagedMembers.continuationToken;
                members.push(...pagedMembers.members);
            }
            while(continuationToken !== undefined)

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="5fdc6-114">Python</span><span class="sxs-lookup"><span data-stu-id="5fdc6-114">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="5fdc6-115">JSON</span><span class="sxs-lookup"><span data-stu-id="5fdc6-115">JSON</span></span>](#tab/json)

<span data-ttu-id="5fdc6-116">Vous pouvez directement émettre une requête GET sur `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` , en utilisant la valeur de `serviceUrl` comme point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-116">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="5fdc6-117">La valeur de `serviceUrl` tend à être stable mais peut varier.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-117">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5fdc6-118">Lorsqu’un nouveau message arrive, votre robot doit vérifier sa valeur stockée pour `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="5fdc6-118">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
    "continuationToken": "asdfqwerueiqpiewr",
    "members":
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
}
```

* * *

## <a name="get-single-member-details"></a><span data-ttu-id="5fdc6-119">Obtenir les détails d’un membre unique</span><span class="sxs-lookup"><span data-stu-id="5fdc6-119">Get single member details</span></span>

<span data-ttu-id="5fdc6-120">Vous pouvez également récupérer les détails d’un utilisateur particulier à l’aide de son ID d’utilisateur Teams, de son UPN ou de son ID d’objet AAD.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-120">You can also retrieve the details of a particular user using their Teams user Id, UPN, or AAD Object Id.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5fdc6-121">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5fdc6-121">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5fdc6-122">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5fdc6-122">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        const member = await TeamsInfo.getMember(context, encodeURI('someone@somecompany.com'));

        // By calling next() you ensure that the next BotHandler is run.
        await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="5fdc6-123">Python</span><span class="sxs-lookup"><span data-stu-id="5fdc6-123">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="5fdc6-124">JSON</span><span class="sxs-lookup"><span data-stu-id="5fdc6-124">JSON</span></span>](#tab/json)

<span data-ttu-id="5fdc6-125">Vous pouvez directement émettre une requête GET sur `/v3/conversations/{conversationId}/members/{userId}` , en utilisant la valeur de `serviceUrl` comme point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-125">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="5fdc6-126">La valeur de `serviceUrl` tend à être stable mais peut varier.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-126">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5fdc6-127">Lorsqu’un nouveau message arrive, votre robot doit vérifier sa valeur stockée pour `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="5fdc6-127">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/labrown@fabrikam.com"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}
```

* * *

## <a name="get-teams-details"></a><span data-ttu-id="5fdc6-128">Obtenir les détails de l’équipe</span><span class="sxs-lookup"><span data-stu-id="5fdc6-128">Get team's details</span></span>

<span data-ttu-id="5fdc6-129">Lorsqu’il est installé dans une équipe, votre bot peut interroger des métadonnées sur cette équipe, y compris sur Azure AD groupId.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-129">When installed in a team, your bot can query for metadata about that team including the Azure AD groupId.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5fdc6-130">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5fdc6-130">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        TeamDetails teamDetails = await TeamsInfo.GetTeamDetailsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);
        if (teamDetails != null) {
            await turnContext.SendActivityAsync($"The groupId is: {teamDetails.AadGroupId}");
        }
        else {
            await turnContext.SendActivityAsync($"Message did not come from a channel in a team.");
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5fdc6-131">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5fdc6-131">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const teamDetails = await TeamsInfo.getTeamDetails(turnContext);
            if (teamDetails) {
                await turnContext.sendActivity(`The group ID is: ${teamDetails.aadGroupId}`);
            } else {
                await turnContext.sendActivity('This message did not come from a channel in a team.');
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="5fdc6-132">Python</span><span class="sxs-lookup"><span data-stu-id="5fdc6-132">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="5fdc6-133">JSON</span><span class="sxs-lookup"><span data-stu-id="5fdc6-133">JSON</span></span>](#tab/json)

<span data-ttu-id="5fdc6-134">Vous pouvez directement émettre une requête GET sur `/v3/teams/{teamId}` , en utilisant la valeur de `serviceUrl` comme point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-134">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="5fdc6-135">La valeur de `serviceUrl` tend à être stable mais peut varier.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-135">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5fdc6-136">Lorsqu’un nouveau message arrive, votre robot doit vérifier sa valeur stockée pour `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="5fdc6-136">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/teams/19:ja0cu120i1jod12j@skype.net

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "The Team Name",
    "aadGroupId": "02ce3874-dd86-41ba-bddc-013f34019978"
}
```

* * *

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="5fdc6-137">Obtenir la liste des canaux dans une équipe</span><span class="sxs-lookup"><span data-stu-id="5fdc6-137">Get the list of channels in a team</span></span>

<span data-ttu-id="5fdc6-138">Votre robot peut interroger la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-138">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="5fdc6-139">Le nom du canal général par défaut est renvoyé en tant que `null` pour permettre la localisation.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-139">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="5fdc6-140">L’ID de canal pour le canal général correspond toujours à l’ID d’équipe.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-140">The channel ID for the General channel always matches the team ID.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="5fdc6-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="5fdc6-141">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        IEnumerable<ChannelInfo> channels = await TeamsInfo.GetTeamChannelsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);

        await turnContext.SendActivityAsync($"The channel count is: {channels.Count()}");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="5fdc6-142">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="5fdc6-142">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const channels = await TeamsInfo.getTeamChannels(turnContext);

            await turnContext.sendActivity(`The channel count is: ${channels.length}`);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="5fdc6-143">Python</span><span class="sxs-lookup"><span data-stu-id="5fdc6-143">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="5fdc6-144">JSON</span><span class="sxs-lookup"><span data-stu-id="5fdc6-144">JSON</span></span>](#tab/json)

<span data-ttu-id="5fdc6-145">Vous pouvez directement émettre une requête GET sur `/v3/teams/{teamId}/conversations` , en utilisant la valeur de `serviceUrl` comme point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-145">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="5fdc6-146">La valeur de `serviceUrl` tend à être stable mais peut varier.</span><span class="sxs-lookup"><span data-stu-id="5fdc6-146">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="5fdc6-147">Lorsqu’un nouveau message arrive, votre robot doit vérifier sa valeur stockée pour `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="5fdc6-147">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
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

* * *

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
