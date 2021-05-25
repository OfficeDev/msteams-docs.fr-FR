---
title: Obtenir Teams contexte spécifique pour votre bot
author: laujan
description: Comment obtenir le contexte spécifique de Microsoft Team pour votre bot, y compris la liste des conversations, les détails et la liste des canaux.
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 6a8f903fb2f3ed8120e31b7536b65f22fdf6d620
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630165"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="c4fe4-103">Obtenir Teams contexte spécifique pour votre bot</span><span class="sxs-lookup"><span data-stu-id="c4fe4-103">Get Teams specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="c4fe4-104">Un bot peut accéder à des données de contexte supplémentaires sur une équipe ou une conversation sur laquelle il est installé.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-104">A bot can access additional context data about a team or chat where it is installed.</span></span> <span data-ttu-id="c4fe4-105">Ces informations peuvent être utilisées pour enrichir les fonctionnalités du bot et fournir une expérience plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetch-the-roster-or-user-profile"></a><span data-ttu-id="c4fe4-106">Récupérer la liste ou le profil utilisateur</span><span class="sxs-lookup"><span data-stu-id="c4fe4-106">Fetch the roster or user profile</span></span>

<span data-ttu-id="c4fe4-107">Votre bot peut interroger la liste des membres et leurs profils utilisateur de base, notamment les ID d’utilisateur Teams et les informations de Azure Active Directory (AAD), telles que le nom et objectId.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-107">Your bot can query for the list of members and their basic user profiles, including Teams user IDs and Azure Active Directory (AAD) information, such as name and objectId.</span></span> <span data-ttu-id="c4fe4-108">Vous pouvez utiliser ces informations pour corréler les identités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-108">You can use this information to correlate user identities.</span></span> <span data-ttu-id="c4fe4-109">Par exemple, pour vérifier si un utilisateur s’est connecté à un onglet via les informations d’identification AAD, est membre de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-109">For example, to check whether a user logged into a tab through AAD credentials, is a member of the team.</span></span> <span data-ttu-id="c4fe4-110">Pour obtenir les membres de la conversation, la taille de page minimale ou maximale dépend de l’implémentation.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-110">For get conversation members, minimum or maximum page size depends on the implementation.</span></span> <span data-ttu-id="c4fe4-111">La taille de page inférieure à 50, traitée comme 50 et supérieure à 500, est limitée à 500.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-111">Page size less than 50, are treated as 50, and greater than 500, are capped at 500.</span></span> <span data-ttu-id="c4fe4-112">Même si vous utilisez la version non pagyée, elle n’est pas fiable dans les grandes équipes et ne doit pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-112">Even if you use the non-paged version, it is unreliable in large teams and must not be used.</span></span> <span data-ttu-id="c4fe4-113">Pour plus d’informations, voir [les modifications apportées aux API Teams bot pour](~/resources/team-chat-member-api-changes.md)récupérer des membres d’équipe ou de conversation.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-113">For more information, see [changes to Teams Bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="c4fe4-114">L’exemple de code suivant utilise le point de terminaison pagé pour extraire la liste :</span><span class="sxs-lookup"><span data-stu-id="c4fe4-114">The following sample code uses the paged endpoint for fetching the roster:</span></span>

# <a name="c"></a>[<span data-ttu-id="c4fe4-115">C#</span><span class="sxs-lookup"><span data-stu-id="c4fe4-115">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="c4fe4-116">TypeScript</span><span class="sxs-lookup"><span data-stu-id="c4fe4-116">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="c4fe4-117">Python</span><span class="sxs-lookup"><span data-stu-id="c4fe4-117">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="c4fe4-118">JSON</span><span class="sxs-lookup"><span data-stu-id="c4fe4-118">JSON</span></span>](#tab/json)

<span data-ttu-id="c4fe4-119">Vous pouvez émettre directement une requête GET sur , en utilisant la `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` valeur de comme point de `serviceUrl` terminaison.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-119">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="c4fe4-120">La valeur de `serviceUrl` est stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-120">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="c4fe4-121">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée pour `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="c4fe4-121">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="c4fe4-122">La charge utile de réponse indique également si l’utilisateur est un utilisateur normal ou anonyme.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-122">The response payload also indicates if the user is a regular or anonymous user.</span></span>

```http
GET /v3/conversations/19:meeting_N2QzYTA3YmItYmMwOC00OTJmLThkYzMtZWMzZGU0NGIyZGI0@thread.v2/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
   "continuationToken":"asdfqwerueiqpiewr",
   "members":[
      {
         "id":"29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
         "name":"Anon1 (Guest)",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"anonymous"
      },
      {
         "id":"29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
         "objectId":"76b0b09f-d410-48fd-993e-84da521a597b",
         "givenName":"John",
         "surname":"Patterson",
         "email":"johnp@fabrikam.com",
         "userPrincipalName":"johnp@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      },
      {
         "id":"29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
         "objectId":"6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
         "givenName":"Rick",
         "surname":"Stevens",
         "email":"Rick.Stevens@fabrikam.com",
         "userPrincipalName":"rstevens@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      }
   ]
}
```

* * *

<span data-ttu-id="c4fe4-123">Après avoir récupéré la liste ou le profil utilisateur, vous pouvez obtenir les détails d’un seul membre.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-123">After you fetch the roster or user profile, you can get details of a single member.</span></span> <span data-ttu-id="c4fe4-124">Actuellement, pour récupérer des informations pour un ou plusieurs membres d’une conversation ou d’une équipe, utilisez les API Microsoft Teams bot pour C# ou pour les `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` API TypeScript.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-124">Currently, to retrieve information for one or more members of a chat or team, use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript APIs.</span></span>

## <a name="get-single-member-details"></a><span data-ttu-id="c4fe4-125">Obtenir les détails d’un seul membre</span><span class="sxs-lookup"><span data-stu-id="c4fe4-125">Get single member details</span></span>

<span data-ttu-id="c4fe4-126">Vous pouvez également récupérer les détails d’un utilisateur particulier à l’aide Teams ID d’utilisateur, UPN ou ID d’objet AAD.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-126">You can also retrieve the details of a particular user using their Teams user ID, UPN, or AAD Object ID.</span></span>

<span data-ttu-id="c4fe4-127">L’exemple de code suivant est utilisé pour obtenir les détails d’un seul membre :</span><span class="sxs-lookup"><span data-stu-id="c4fe4-127">The following sample code is used to get single member details:</span></span>

# <a name="c"></a>[<span data-ttu-id="c4fe4-128">C#</span><span class="sxs-lookup"><span data-stu-id="c4fe4-128">C#</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="c4fe4-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="c4fe4-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="c4fe4-130">Python</span><span class="sxs-lookup"><span data-stu-id="c4fe4-130">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="c4fe4-131">JSON</span><span class="sxs-lookup"><span data-stu-id="c4fe4-131">JSON</span></span>](#tab/json)

<span data-ttu-id="c4fe4-132">Vous pouvez émettre directement une requête GET sur , en utilisant la `/v3/conversations/{conversationId}/members/{userId}` valeur de comme point de `serviceUrl` terminaison.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-132">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="c4fe4-133">La valeur de `serviceUrl` est stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-133">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="c4fe4-134">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée pour `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="c4fe4-134">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="c4fe4-135">Cela peut être utilisé pour les utilisateurs ordinaires et les utilisateurs anonymes.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-135">This can be used for regular users and anonymous users.</span></span>

<span data-ttu-id="c4fe4-136">Voici l’exemple de réponse pour un utilisateur normal :</span><span class="sxs-lookup"><span data-stu-id="c4fe4-136">The following is the response sample for regular user:</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"user"
}
```

<span data-ttu-id="c4fe4-137">Voici l’exemple de réponse pour l’utilisateur anonyme :</span><span class="sxs-lookup"><span data-stu-id="c4fe4-137">The following is the response sample for anonymous user:</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/<anonymous user id>"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"anonymous"
}
```

* * *

<span data-ttu-id="c4fe4-138">Une fois que vous avez obtenir les détails d’un seul membre, vous pouvez obtenir les détails de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-138">After you get details of a single member, you can get details of the team.</span></span> <span data-ttu-id="c4fe4-139">Actuellement, pour récupérer des informations pour une équipe, utilisez les API Microsoft Teams bot pour C# `TeamsInfo.GetMemberDetailsAsync` ou `TeamsInfo.getTeamDetails` TypeScript.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-139">Currently, to retrieve information for a team, use the Microsoft Teams bot APIs `TeamsInfo.GetMemberDetailsAsync` for C# or `TeamsInfo.getTeamDetails` for TypeScript.</span></span>

## <a name="get-teams-details"></a><span data-ttu-id="c4fe4-140">Obtenir les détails de l’équipe</span><span class="sxs-lookup"><span data-stu-id="c4fe4-140">Get team's details</span></span>

<span data-ttu-id="c4fe4-141">Lorsqu’il est installé dans une équipe, votre bot peut interroger des métadonnées sur cette équipe, y compris l’ID de groupe AAD.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-141">When installed in a team, your bot can query for metadata about that team including the AAD group ID.</span></span>

<span data-ttu-id="c4fe4-142">L’exemple de code suivant est utilisé pour obtenir les détails de l’équipe :</span><span class="sxs-lookup"><span data-stu-id="c4fe4-142">The following sample code is used to get team's details:</span></span>

# <a name="c"></a>[<span data-ttu-id="c4fe4-143">C#</span><span class="sxs-lookup"><span data-stu-id="c4fe4-143">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="c4fe4-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="c4fe4-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="c4fe4-145">Python</span><span class="sxs-lookup"><span data-stu-id="c4fe4-145">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="c4fe4-146">JSON</span><span class="sxs-lookup"><span data-stu-id="c4fe4-146">JSON</span></span>](#tab/json)

<span data-ttu-id="c4fe4-147">Vous pouvez émettre directement une requête GET sur , en utilisant la `/v3/teams/{teamId}` valeur de comme point de `serviceUrl` terminaison.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-147">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="c4fe4-148">La valeur de `serviceUrl` est stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-148">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="c4fe4-149">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée pour `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="c4fe4-149">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

<span data-ttu-id="c4fe4-150">Une fois que vous avez obtenir les détails de l’équipe, vous pouvez obtenir la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-150">After you get details of the team, you can get the list of channels in a team.</span></span> <span data-ttu-id="c4fe4-151">Actuellement, pour récupérer des informations pour une liste de canaux dans une équipe, utilisez les API de bot Microsoft Teams pour C# ou pour les `TeamsInfo.GetTeamChannelsAsync` `TeamsInfo.getTeamChannels` API TypeScript.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-151">Currently, to retrieve information for a list of channels in a team, use the Microsoft Teams bot APIs `TeamsInfo.GetTeamChannelsAsync` for C# or `TeamsInfo.getTeamChannels` for TypeScript APIs.</span></span>

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="c4fe4-152">Obtenir la liste des canaux d’une équipe</span><span class="sxs-lookup"><span data-stu-id="c4fe4-152">Get the list of channels in a team</span></span>

<span data-ttu-id="c4fe4-153">Votre bot peut interroger la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-153">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
> * <span data-ttu-id="c4fe4-154">Le nom du canal général par défaut est renvoyé pour `null` autoriser la localisation.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-154">The name of the default General channel is returned as `null` to allow for localization.</span></span>
> * <span data-ttu-id="c4fe4-155">L’ID de canal pour le canal général correspond toujours à l’ID d’équipe.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-155">The channel ID for the General channel always matches the team ID.</span></span>

<span data-ttu-id="c4fe4-156">L’exemple de code suivant est utilisé pour obtenir la liste des canaux d’une équipe :</span><span class="sxs-lookup"><span data-stu-id="c4fe4-156">The following sample code is used to get the list of channels in a team:</span></span>

# <a name="c"></a>[<span data-ttu-id="c4fe4-157">C#</span><span class="sxs-lookup"><span data-stu-id="c4fe4-157">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="c4fe4-158">TypeScript</span><span class="sxs-lookup"><span data-stu-id="c4fe4-158">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="c4fe4-159">Python</span><span class="sxs-lookup"><span data-stu-id="c4fe4-159">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="c4fe4-160">JSON</span><span class="sxs-lookup"><span data-stu-id="c4fe4-160">JSON</span></span>](#tab/json)

<span data-ttu-id="c4fe4-161">Vous pouvez émettre directement une requête GET sur , en utilisant la `/v3/teams/{teamId}/conversations` valeur de comme point de `serviceUrl` terminaison.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-161">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="c4fe4-162">La valeur de `serviceUrl` est stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="c4fe4-162">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="c4fe4-163">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée pour `serviceUrl` .</span><span class="sxs-lookup"><span data-stu-id="c4fe4-163">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

## <a name="next-step"></a><span data-ttu-id="c4fe4-164">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="c4fe4-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4fe4-165">Envoyer et recevoir des fichiers via le bot</span><span class="sxs-lookup"><span data-stu-id="c4fe4-165">Send and receive files through the bot</span></span>](~/bots/how-to/bots-filesv4.md)
