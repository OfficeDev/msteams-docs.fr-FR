---
title: Obtenir le contexte de votre bot Microsoft Teams de recherche
description: Décrit comment obtenir du contexte pour les bots dans Microsoft Teams
keywords: contexte des bots teams
ms.topic: conceptual
localization_priority: Normal
ms.date: 05/20/2019
ms.openlocfilehash: cda2e24816330964342b097f52bb955c8846c54a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566487"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a><span data-ttu-id="66dda-104">Obtenir le contexte de votre bot Microsoft Teams de recherche</span><span class="sxs-lookup"><span data-stu-id="66dda-104">Get context for your Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="66dda-105">Votre bot peut accéder à un contexte supplémentaire sur l’équipe ou la conversation, tel que le profil utilisateur.</span><span class="sxs-lookup"><span data-stu-id="66dda-105">Your bot can access additional context about the team or chat, such as user profile.</span></span> <span data-ttu-id="66dda-106">Ces informations peuvent être utilisées pour enrichir les fonctionnalités de votre bot et offrir une expérience plus personnalisée.</span><span class="sxs-lookup"><span data-stu-id="66dda-106">This information can be used to enrich your bot's functionality and provide a more personalized experience.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="66dda-107">Microsoft Teams’API de bot spécifiques sont les plus accessibles via nos extensions pour le SDK Bot Builder.</span><span class="sxs-lookup"><span data-stu-id="66dda-107">Microsoft Teams-specific bot APIs are best accessed through our extensions for the Bot Builder SDK.</span></span>
> * <span data-ttu-id="66dda-108">Pour C# ou .NET, téléchargez notre package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span><span class="sxs-lookup"><span data-stu-id="66dda-108">For C# or .NET, download our [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>
> * <span data-ttu-id="66dda-109">Pour Node.js développement, le Générateur de bot pour Teams est incorporé dans le [SDK Bot Framework](https://github.com/microsoft/botframework-sdk) v4.6.</span><span class="sxs-lookup"><span data-stu-id="66dda-109">For Node.js development, the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.</span></span>

## <a name="fetch-the-team-roster"></a><span data-ttu-id="66dda-110">Récupérer la liste d’équipe</span><span class="sxs-lookup"><span data-stu-id="66dda-110">Fetch the team roster</span></span>

<span data-ttu-id="66dda-111">Votre bot peut interroger la liste des membres de l’équipe et leurs profils de base.</span><span class="sxs-lookup"><span data-stu-id="66dda-111">Your bot can query for the list of team members and their basic profiles.</span></span> <span data-ttu-id="66dda-112">Les profils de base incluent Teams’ID d’utilisateur et des informations Azure Active Directory (AAD), telles que le nom et l’ID d’objet.</span><span class="sxs-lookup"><span data-stu-id="66dda-112">The basic profiles include Teams user IDs and Azure Active Directory (AAD) information such as name and object ID.</span></span> <span data-ttu-id="66dda-113">Vous pouvez utiliser ces informations pour corréler les identités des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="66dda-113">You can use this information to correlate user identities.</span></span> <span data-ttu-id="66dda-114">Par exemple, vérifiez si un utilisateur connecté à un onglet via les informations d’identification AAD est membre de l’équipe.</span><span class="sxs-lookup"><span data-stu-id="66dda-114">For example, check if a user logged into a tab through AAD credentials is a team member.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="66dda-115">Exemple d’API REST</span><span class="sxs-lookup"><span data-stu-id="66dda-115">REST API example</span></span>

<span data-ttu-id="66dda-116">Émettre directement une requête GET sur [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members) , en utilisant la valeur comme point de `serviceUrl` terminaison.</span><span class="sxs-lookup"><span data-stu-id="66dda-116">Directly issue a GET request on [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members), using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="66dda-117">Vous pouvez le trouver dans l’objet de la charge utile d’activité que votre `teamId` `channeldata` bot reçoit dans les scénarios suivants :</span><span class="sxs-lookup"><span data-stu-id="66dda-117">The `teamId` can be found in the `channeldata` object of the activity payload that your bot receives in the following scenarios:</span></span>

* <span data-ttu-id="66dda-118">Lorsqu’un utilisateur échange des messages ou interagit avec votre bot dans un contexte d’équipe.</span><span class="sxs-lookup"><span data-stu-id="66dda-118">When a user messages or interacts with your bot in a team context.</span></span> <span data-ttu-id="66dda-119">Pour plus d’informations, voir [la réception de messages.](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)</span><span class="sxs-lookup"><span data-stu-id="66dda-119">For more information, see [receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages).</span></span>
* <span data-ttu-id="66dda-120">Lorsqu’un nouvel utilisateur ou bot est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="66dda-120">When a new user or bot is added to a team.</span></span> <span data-ttu-id="66dda-121">Pour plus d’informations, [voir bot ou utilisateur ajouté à une équipe.](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)</span><span class="sxs-lookup"><span data-stu-id="66dda-121">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team).</span></span>

> [!NOTE]
>
>* <span data-ttu-id="66dda-122">Utilisez toujours l’ID d’équipe lors de l’appel de l’API.</span><span class="sxs-lookup"><span data-stu-id="66dda-122">Always use the team ID when calling the API.</span></span>
>* <span data-ttu-id="66dda-123">La `serviceUrl` valeur tend à être stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="66dda-123">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="66dda-124">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur `serviceUrl` stockée.</span><span class="sxs-lookup"><span data-stu-id="66dda-124">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

### <a name="net-example"></a><span data-ttu-id="66dda-125">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="66dda-125">.NET example</span></span>

<span data-ttu-id="66dda-126">Appel `GetConversationMembersAsync` utilisé `Team.Id` pour renvoyer une liste d’ID d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="66dda-126">Call `GetConversationMembersAsync` using `Team.Id` to return a list of user IDs.</span></span>

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

### <a name="nodejs-or-typescript-example"></a><span data-ttu-id="66dda-127">Node.js exemple ou TypeScript</span><span class="sxs-lookup"><span data-stu-id="66dda-127">Node.js or TypeScript example</span></span>

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a><span data-ttu-id="66dda-128">Récupérer le profil ou la liste d’utilisateurs dans une conversation personnelle ou de groupe</span><span class="sxs-lookup"><span data-stu-id="66dda-128">Fetch user profile or roster in personal or group chat</span></span>

<span data-ttu-id="66dda-129">Vous pouvez appeler l’API pour toute conversation personnelle afin d’obtenir les informations de profil de l’utilisateur qui discute avec votre bot.</span><span class="sxs-lookup"><span data-stu-id="66dda-129">You can make the API call for any personal chat to obtain the profile information of the user chatting with your bot.</span></span>

<span data-ttu-id="66dda-130">L’appel d’API, les méthodes du SDK et l’objet de réponse sont identiques à la récupération de la liste d’équipe.</span><span class="sxs-lookup"><span data-stu-id="66dda-130">The API call, SDK methods, and the response object are identical to fetching the team roster.</span></span> <span data-ttu-id="66dda-131">La seule différence est que vous passez le `conversationId` . `teamId`</span><span class="sxs-lookup"><span data-stu-id="66dda-131">The only difference is you pass the `conversationId` instead of the `teamId`.</span></span>

## <a name="fetch-the-list-of-channels-in-a-team"></a><span data-ttu-id="66dda-132">Récupérer la liste des canaux d’une équipe</span><span class="sxs-lookup"><span data-stu-id="66dda-132">Fetch the list of channels in a team</span></span>

<span data-ttu-id="66dda-133">Votre bot peut interroger la liste des canaux d’une équipe.</span><span class="sxs-lookup"><span data-stu-id="66dda-133">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="66dda-134">Le nom du canal général par défaut est renvoyé pour `null` autoriser la localisation.</span><span class="sxs-lookup"><span data-stu-id="66dda-134">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="66dda-135">L’ID de canal pour le canal général correspond toujours à l’ID d’équipe.</span><span class="sxs-lookup"><span data-stu-id="66dda-135">The channel ID for the General channel always matches the team ID.</span></span>

### <a name="rest-api-example"></a><span data-ttu-id="66dda-136">Exemple d’API REST</span><span class="sxs-lookup"><span data-stu-id="66dda-136">REST API example</span></span>

<span data-ttu-id="66dda-137">Émettre directement une requête GET sur `/teams/{teamId}/conversations/` , en utilisant la valeur comme point de `serviceUrl` terminaison.</span><span class="sxs-lookup"><span data-stu-id="66dda-137">Directly issue a GET request on `/teams/{teamId}/conversations/`, using the `serviceUrl` value as the endpoint.</span></span>

<span data-ttu-id="66dda-138">La seule source est `teamId` un message du contexte d’équipe.</span><span class="sxs-lookup"><span data-stu-id="66dda-138">The only source for `teamId` is a message from the team context.</span></span> <span data-ttu-id="66dda-139">Le message est un message d’un utilisateur ou le message que votre bot reçoit lorsqu’il est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="66dda-139">The message is either a message from a user or the message that your bot receives when it is added to a team.</span></span> <span data-ttu-id="66dda-140">Pour plus d’informations, [voir bot ou utilisateur ajouté à une équipe.](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)</span><span class="sxs-lookup"><span data-stu-id="66dda-140">For more information, see [bot or user added to a team](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition).</span></span>

> [!NOTE]
> <span data-ttu-id="66dda-141">La `serviceUrl` valeur tend à être stable, mais peut changer.</span><span class="sxs-lookup"><span data-stu-id="66dda-141">The `serviceUrl` value tends to be stable but can change.</span></span> <span data-ttu-id="66dda-142">Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur `serviceUrl` stockée.</span><span class="sxs-lookup"><span data-stu-id="66dda-142">When a new message arrives, your bot must verify its stored `serviceUrl` value.</span></span>

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

#### <a name="net-example"></a><span data-ttu-id="66dda-143">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="66dda-143">.NET example</span></span>

<span data-ttu-id="66dda-144">L’exemple suivant utilise l’appel des extensions Teams pour le `FetchChannelList` [SDK Bot Builder pour .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span><span class="sxs-lookup"><span data-stu-id="66dda-144">The following example uses the `FetchChannelList` call from the [Teams extensions for the Bot Builder SDK for .NET](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams):</span></span>

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a><span data-ttu-id="66dda-145">Node.js exemple</span><span class="sxs-lookup"><span data-stu-id="66dda-145">Node.js example</span></span>

<span data-ttu-id="66dda-146">L’exemple suivant utilise `fetchChannelList` l’appel des extensions Teams pour le [SDK Bot Builder pour Node.js](https://www.npmjs.com/package/botbuilder-teams):</span><span class="sxs-lookup"><span data-stu-id="66dda-146">The following example uses `fetchChannelList` call from the [Teams extensions for the Bot Builder SDK for Node.js](https://www.npmjs.com/package/botbuilder-teams):</span></span>

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

## <a name="get-clientinfo-in-your-bot-context"></a><span data-ttu-id="66dda-147">Obtenir clientInfo dans le contexte de votre bot</span><span class="sxs-lookup"><span data-stu-id="66dda-147">Get clientInfo in your bot context</span></span>

<span data-ttu-id="66dda-148">Vous pouvez extraire le clientInfo au sein de l’activité de votre bot.</span><span class="sxs-lookup"><span data-stu-id="66dda-148">You can fetch the clientInfo within your bot's activity.</span></span> <span data-ttu-id="66dda-149">ClientInfo contient les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="66dda-149">The clientInfo contains the following properties:</span></span>

* <span data-ttu-id="66dda-150">Locale</span><span class="sxs-lookup"><span data-stu-id="66dda-150">Locale</span></span>
* <span data-ttu-id="66dda-151">Pays</span><span class="sxs-lookup"><span data-stu-id="66dda-151">Country</span></span>
* <span data-ttu-id="66dda-152">Plateforme</span><span class="sxs-lookup"><span data-stu-id="66dda-152">Platform</span></span>
* <span data-ttu-id="66dda-153">Fuseau horaire</span><span class="sxs-lookup"><span data-stu-id="66dda-153">Timezone</span></span>

### <a name="json-example"></a><span data-ttu-id="66dda-154">Exemple JSON</span><span class="sxs-lookup"><span data-stu-id="66dda-154">JSON example</span></span>

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

### <a name="c-example"></a><span data-ttu-id="66dda-155">C# exemple</span><span class="sxs-lookup"><span data-stu-id="66dda-155">C# example</span></span>

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a><span data-ttu-id="66dda-156">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="66dda-156">See also</span></span>

<span data-ttu-id="66dda-157">[Exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="66dda-157">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>