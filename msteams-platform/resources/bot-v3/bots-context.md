---
title: Obtenir le contexte de votre robot
description: Décrit comment obtenir le contexte des robots dans Microsoft teams
keywords: contexte des robots teams
ms.date: 05/20/2019
ms.openlocfilehash: 2dea6fd51e7274fa899d9ae882441a21618d7e09
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41674024"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="93cd2-104">Obtenir le contexte de votre robot Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="93cd2-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="93cd2-105">Votre robot peut accéder à un contexte supplémentaire concernant l’équipe ou la conversation, comme le profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="93cd2-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="93cd2-106">Ces informations peuvent être utilisées pour enrichir les fonctionnalités de votre robot et fournir une expérience plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="93cd2-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
> <span data-ttu-id="93cd2-107">Ces API de&ndash;robot spécifiques de Microsoft teams sont les meilleurs accessibles via nos extensions pour le kit de développement logiciel (SDK) du générateur de robots.</span><span class="sxs-lookup"><span data-stu-id="93cd2-107">These Microsoft Teams&ndash;specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span> <span data-ttu-id="93cd2-108">Pour C#/.NET, téléchargez notre package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="93cd2-108">For C#/.NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span> <span data-ttu-id="93cd2-109">Pour le développement de node. js, vous pouvez installer le package NPM [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) .</span><span class="sxs-lookup"><span data-stu-id="93cd2-109">For Node.js development, you can install the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span> <span data-ttu-id="93cd2-110">Les deux SDK Target Builder v3.</span><span class="sxs-lookup"><span data-stu-id="93cd2-110">Both SDKs target Bot Builder v3.</span></span>

## <a name="fetching-the-team-roster"></a><span data-ttu-id="93cd2-111">Extraction de la liste de l’équipe</span><span class="sxs-lookup"><span data-stu-id="93cd2-111">Fetching the team roster</span></span>

<span data-ttu-id="93cd2-112">Votre robot peut demander la liste des membres de l’équipe et leurs profils de base, qui incluent les ID utilisateur teams et les informations Azure Active Directory (Azure AD), telles que nom et objectId.</span><span class="sxs-lookup"><span data-stu-id="93cd2-112">Your bot can query for the list of team members and their basic profiles, which includes Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="93cd2-113">Vous pouvez utiliser ces informations pour corréler les identités des utilisateurs ; par exemple, pour vérifier si un utilisateur connecté à un onglet par le biais d’informations d’identification Azure AD est membre de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="93cd2-113">You can use this information to correlate user identities; for example, to check whether a user logged into a tab through Azure AD credentials is a member of the team.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="93cd2-114">Exemple d’API REST</span><span class="sxs-lookup"><span data-stu-id="93cd2-114">REST API example</span></span>

<span data-ttu-id="93cd2-115">Vous pouvez directement émettre une requête GET sur [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), en utilisant la valeur `serviceUrl` de comme point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="93cd2-115">You can directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="93cd2-116">Le `teamId` peut être trouvé dans l' `channeldata` objet de la charge utile d’activité que votre robot reçoit dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="93cd2-116">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>
* <span data-ttu-id="93cd2-117">Quand un utilisateur entre ou interagit avec votre robot dans un contexte d’équipe (voir [réception de messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span><span class="sxs-lookup"><span data-stu-id="93cd2-117">When a user messages or interacts with your bot in a team context (see [Receiving Messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages))</span></span>
* <span data-ttu-id="93cd2-118">Lorsqu’un nouvel utilisateur ou robot est ajouté à une équipe (voir [bot ou User ajouté à une équipe](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span><span class="sxs-lookup"><span data-stu-id="93cd2-118">When a new user or bot is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team))</span></span>

> [!NOTE]
>* <span data-ttu-id="93cd2-119">Veillez à utiliser l’ID d’équipe lors de l’appel de l’API.</span><span class="sxs-lookup"><span data-stu-id="93cd2-119">Make sure to use the team id when calling the api</span></span>
>* <span data-ttu-id="93cd2-120">La valeur de `serviceUrl` tend à être stable mais peut varier.</span><span class="sxs-lookup"><span data-stu-id="93cd2-120">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="93cd2-121">Lors de l’arrivée d’un nouveau message, votre robot doit vérifier sa `serviceUrl`valeur stockée.</span><span class="sxs-lookup"><span data-stu-id="93cd2-121">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="93cd2-122">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="93cd2-122">.NET example</span></span>

<span data-ttu-id="93cd2-123">Appelez `GetConversationMembersAsync` using `Team.Id` pour renvoyer la liste des ID d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="93cd2-123">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejstypescript-example"></a><span data-ttu-id="93cd2-124">Exemple node. js/machine à écrire</span><span class="sxs-lookup"><span data-stu-id="93cd2-124">Node.js/TypeScript example</span></span>

<span data-ttu-id="93cd2-125">L’exemple suivant utilise les [extensions Microsoft teams pour le kit de développement logiciel (SDK) du générateur de robots pour node. js](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="93cd2-125">The following example uses the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

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

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="93cd2-126">Extraction d’un profil utilisateur ou d’une liste dans la conversation personnelle ou de groupe</span><span class="sxs-lookup"><span data-stu-id="93cd2-126">Fetching user profile or roster in personal or group chat</span></span>

<span data-ttu-id="93cd2-127">Vous pouvez également effectuer la même appel d’API pour toute conversation personnelle afin d’obtenir les informations de profil de l’utilisateur en conversation avec votre robot.</span><span class="sxs-lookup"><span data-stu-id="93cd2-127">You can also make the same API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="93cd2-128">Les méthodes de l’appel de l’API et du kit de développement logiciel sont identiques à la récupération de la liste de l’équipe, comme l’est l’objet de réponse.</span><span class="sxs-lookup"><span data-stu-id="93cd2-128">The API call and SDK methods are identical to fetching the team roster, as is the response object.</span></span> <span data-ttu-id="93cd2-129">La seule différence est que vous transmettez la `conversationId` à `teamId`la place de.</span><span class="sxs-lookup"><span data-stu-id="93cd2-129">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetching-the-list-of-channels-in-a-team"></a><span data-ttu-id="93cd2-130">Extraction de la liste des canaux dans une équipe</span><span class="sxs-lookup"><span data-stu-id="93cd2-130">Fetching the list of channels in a team</span></span>

<span data-ttu-id="93cd2-131">Votre robot peut interroger la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="93cd2-131">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="93cd2-132">Le nom du canal général par défaut est renvoyé en `null` tant que pour permettre la localisation.</span><span class="sxs-lookup"><span data-stu-id="93cd2-132">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="93cd2-133">L’ID de canal pour le canal général correspond toujours à l’ID d’équipe.</span><span class="sxs-lookup"><span data-stu-id="93cd2-133">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="93cd2-134">Exemple d’API REST</span><span class="sxs-lookup"><span data-stu-id="93cd2-134">REST API example</span></span>

<span data-ttu-id="93cd2-135">Vous pouvez directement émettre une requête GET sur `/teams/{teamId}/conversations/`, en utilisant la valeur `serviceUrl` de comme point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="93cd2-135">You can directly issue a GET request on `/teams/{teamId}/conversations/`, using the value of `serviceUrl` as the endpoint.</span></span>

<span data-ttu-id="93cd2-136">La seule source pour `teamId` est un message provenant du contexte de l’équipe, c’est-à-dire un message provenant d’un utilisateur ou d’un message que votre bot reçoit lorsqu’il est ajouté à une équipe (voir [bot ou User ajouté à une équipe](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span><span class="sxs-lookup"><span data-stu-id="93cd2-136">The only source for `teamId` is a message from the team context - either a message from a user or the message that your bot receives when it is added to a team (see [Bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)).</span></span>

> [!NOTE]
> <span data-ttu-id="93cd2-137">La valeur de `serviceUrl` tend à être stable mais peut varier.</span><span class="sxs-lookup"><span data-stu-id="93cd2-137">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="93cd2-138">Lors de l’arrivée d’un nouveau message, votre robot doit vérifier sa `serviceUrl`valeur stockée.</span><span class="sxs-lookup"><span data-stu-id="93cd2-138">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="93cd2-139">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="93cd2-139">.NET example</span></span>

<span data-ttu-id="93cd2-140">L’exemple suivant utilise l' `FetchChannelList` appel de la part des [extensions de Microsoft teams pour le kit de développement logiciel (SDK) du générateur de robots pour .net](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span><span class="sxs-lookup"><span data-stu-id="93cd2-140">The following example uses the `FetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="93cd2-141">Exemple node. js</span><span class="sxs-lookup"><span data-stu-id="93cd2-141">Node.js example</span></span>

<span data-ttu-id="93cd2-142">L’exemple suivant utilise `fetchChannelList` Call à partir des [extensions Microsoft teams pour le kit de développement logiciel (SDK) du générateur de robots pour node. js](https://www.npmjs.com/package/botbuilder-teams).</span><span class="sxs-lookup"><span data-stu-id="93cd2-142">The following example uses `fetchChannelList` call from the [Microsoft Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams).</span></span>

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
