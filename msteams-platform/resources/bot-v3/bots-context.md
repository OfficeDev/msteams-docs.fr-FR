---
title: Obtenir le contexte de votre bot Microsoft Teams
description: Décrit comment obtenir du contexte pour les bots dans Microsoft Teams
keywords: contexte des bots teams
ms.date: 05/20/2019
ms.openlocfilehash: 1465e6624b4eaadd73e2d4d9cf87fccedc002e52
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231549"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="dc25f-104">Obtenir le contexte de votre bot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="dc25f-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="dc25f-105">Votre bot peut accéder à un contexte supplémentaire sur l’équipe ou la conversation, tel que le profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dc25f-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="dc25f-106">Ces informations peuvent être utilisées pour enrichir les fonctionnalités de votre bot et offrir une expérience plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="dc25f-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="dc25f-107">Les API de bot propres à Microsoft Teams sont les plus accessibles via nos extensions pour le SDK Bot Builder.</span><span class="sxs-lookup"><span data-stu-id="dc25f-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="dc25f-108">Pour C# ou .NET, téléchargez notre package [NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="dc25f-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="dc25f-109">Pour Node.js développement, la fonctionnalité Bot Builder pour Teams est incorporée au [SDK Bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.</span><span class="sxs-lookup"><span data-stu-id="dc25f-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="dc25f-110">Récupérer la liste d’équipe</span><span class="sxs-lookup"><span data-stu-id="dc25f-110">Fetch the team roster</span></span>

<span data-ttu-id="dc25f-111">Votre bot peut interroger la liste des membres de l’équipe et leurs profils de base.</span><span class="sxs-lookup"><span data-stu-id="dc25f-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="dc25f-112">Les profils de base incluent les ID d’utilisateur Teams et les informations Azure Active Directory (AAD), telles que le nom et l’ID d’objet.</span><span class="sxs-lookup"><span data-stu-id="dc25f-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="dc25f-113">Vous pouvez utiliser ces informations pour corréler les identités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dc25f-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="dc25f-114">Par exemple, vérifiez si un utilisateur connecté à un onglet via les informations d’identification AAD est membre de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="dc25f-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="dc25f-115">Exemple d’API REST</span><span class="sxs-lookup"><span data-stu-id="dc25f-115">REST API example</span></span>

<span data-ttu-id="dc25f-116">Émettre directement une requête GET sur [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) , en utilisant la valeur comme point de `serviceUrl` terminaison.</span><span class="sxs-lookup"><span data-stu-id="dc25f-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="dc25f-117">Vous pouvez le trouver dans l’objet de la charge utile d’activité que votre `teamId` `channeldata` bot reçoit dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="dc25f-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="dc25f-118">Lorsqu’un utilisateur échange des messages ou interagit avec votre bot dans un contexte d’équipe.</span><span class="sxs-lookup"><span data-stu-id="dc25f-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="dc25f-119">Pour plus d’informations, voir [la réception de messages.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)</span><span class="sxs-lookup"><span data-stu-id="dc25f-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="dc25f-120">Lorsqu’un nouvel utilisateur ou bot est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="dc25f-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="dc25f-121">Pour plus d’informations, [voir bot ou utilisateur ajouté à une équipe.](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)</span><span class="sxs-lookup"><span data-stu-id="dc25f-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="dc25f-122">Utilisez toujours l’ID d’équipe lors de l’appel de l’API.</span><span class="sxs-lookup"><span data-stu-id="dc25f-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="dc25f-123">La `serviceUrl` valeur tend à être stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="dc25f-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="dc25f-124">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur `serviceUrl` stockée.</span><span class="sxs-lookup"><span data-stu-id="dc25f-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="dc25f-125">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="dc25f-125">.NET example</span></span>

<span data-ttu-id="dc25f-126">Appel `GetConversationMembersAsync` utilisé `Team.Id` pour renvoyer une liste d’ID d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="dc25f-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="dc25f-127">Node.js exemple ou TypeScript</span><span class="sxs-lookup"><span data-stu-id="dc25f-127">Node.js or TypeScript example</span></span>

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

<span data-ttu-id="dc25f-128">Voir également les [exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="dc25f-128">Also, see [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="dc25f-129">Récupérer le profil ou la liste d’utilisateurs dans une conversation personnelle ou de groupe</span><span class="sxs-lookup"><span data-stu-id="dc25f-129">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="dc25f-130">Vous pouvez appeler l’API pour toute conversation personnelle afin d’obtenir les informations de profil de l’utilisateur qui discute avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="dc25f-130">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="dc25f-131">L’appel d’API, les méthodes du SDK et l’objet de réponse sont identiques à la récupération de la liste d’équipe.</span><span class="sxs-lookup"><span data-stu-id="dc25f-131">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="dc25f-132">La seule différence est que vous passez le `conversationId` . `teamId`</span><span class="sxs-lookup"><span data-stu-id="dc25f-132">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="dc25f-133">Récupérer la liste des canaux d’une équipe</span><span class="sxs-lookup"><span data-stu-id="dc25f-133">Fetch the list of channels in a team</span></span>

<span data-ttu-id="dc25f-134">Votre bot peut interroger la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="dc25f-134">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="dc25f-135">Le nom du canal général par défaut est renvoyé pour `null` autoriser la localisation.</span><span class="sxs-lookup"><span data-stu-id="dc25f-135">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="dc25f-136">L’ID de canal pour le canal général correspond toujours à l’ID d’équipe.</span><span class="sxs-lookup"><span data-stu-id="dc25f-136">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="dc25f-137">Exemple d’API REST</span><span class="sxs-lookup"><span data-stu-id="dc25f-137">REST API example</span></span>

<span data-ttu-id="dc25f-138">Émettre directement une requête GET sur `/teams/{teamId}/conversations/` , en utilisant la valeur comme point de `serviceUrl` terminaison.</span><span class="sxs-lookup"><span data-stu-id="dc25f-138">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="dc25f-139">La seule source est `teamId` un message du contexte d’équipe.</span><span class="sxs-lookup"><span data-stu-id="dc25f-139">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="dc25f-140">Le message est un message d’un utilisateur ou le message que votre bot reçoit lorsqu’il est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="dc25f-140">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="dc25f-141">Pour plus d’informations, [voir bot ou utilisateur ajouté à une équipe.](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)</span><span class="sxs-lookup"><span data-stu-id="dc25f-141">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="dc25f-142">La `serviceUrl` valeur tend à être stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="dc25f-142">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="dc25f-143">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur `serviceUrl` stockée.</span><span class="sxs-lookup"><span data-stu-id="dc25f-143">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="dc25f-144">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="dc25f-144">.NET example</span></span>

<span data-ttu-id="dc25f-145">L’exemple suivant utilise l’appel des extensions Teams pour le `FetchChannelList` [SDK Bot Builder pour .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span><span class="sxs-lookup"><span data-stu-id="dc25f-145">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="dc25f-146">Node.js exemple</span><span class="sxs-lookup"><span data-stu-id="dc25f-146">Node.js example</span></span>

<span data-ttu-id="dc25f-147">L’exemple suivant utilise l’appel des extensions Teams pour le `fetchChannelList` [SDK Bot Builder Node.js](https://www.npmjs.com/package/botbuilder-teams):</span><span class="sxs-lookup"><span data-stu-id="dc25f-147">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

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

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="dc25f-148">Obtenir clientInfo dans le contexte de votre bot</span><span class="sxs-lookup"><span data-stu-id="dc25f-148">Get clientInfo in your bot context</span></span>

<span data-ttu-id="dc25f-149">Vous pouvez extraire le clientInfo au sein de l’activité de votre bot.</span><span class="sxs-lookup"><span data-stu-id="dc25f-149">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="dc25f-150">ClientInfo contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="dc25f-150">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="dc25f-151">Locale</span><span class="sxs-lookup"><span data-stu-id="dc25f-151">Locale</span></span>
* <span data-ttu-id="dc25f-152">Pays</span><span class="sxs-lookup"><span data-stu-id="dc25f-152">Country</span></span>
* <span data-ttu-id="dc25f-153">Plateforme</span><span class="sxs-lookup"><span data-stu-id="dc25f-153">Platform</span></span>
* <span data-ttu-id="dc25f-154">Fuseau horaire</span><span class="sxs-lookup"><span data-stu-id="dc25f-154">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="dc25f-155">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="dc25f-155">JSON example</span></span>

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

### <a name="c-example"></a><span data-ttu-id="dc25f-156">Exemple C#</span><span class="sxs-lookup"><span data-stu-id="dc25f-156">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```