---
title: Gérer les événements bot
description: Décrit comment gérer les événements dans les robots pour Microsoft teams
keywords: événements bots de teams
ms.date: 05/20/2019
ms.openlocfilehash: 06da5e6b0668e86012d87af3184493cdeb70aecd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673841"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="ecf9a-104">Gérer les événements bot dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="ecf9a-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ecf9a-105">Microsoft teams envoie des notifications à votre bot pour des modifications ou des événements qui se produisent dans les étendues où votre bot est actif.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="ecf9a-106">Vous pouvez utiliser ces événements pour déclencher la logique de service, par exemple :</span><span class="sxs-lookup"><span data-stu-id="ecf9a-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="ecf9a-107">Déclencher un message de bienvenue lorsque votre bot est ajouté à une équipe</span><span class="sxs-lookup"><span data-stu-id="ecf9a-107">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="ecf9a-108">Informations sur les groupes de requêtes et de cache lorsque le bot est ajouté à une conversation de groupe</span><span class="sxs-lookup"><span data-stu-id="ecf9a-108">Query and cache group information when the bot is added to a group chat</span></span>
* <span data-ttu-id="ecf9a-109">Mettre à jour les informations mises en cache sur l’appartenance ou les informations de canal de l’équipe</span><span class="sxs-lookup"><span data-stu-id="ecf9a-109">Update cached information on team membership or channel information</span></span>
* <span data-ttu-id="ecf9a-110">Supprimer les informations mises en cache pour une équipe si le bot est supprimé</span><span class="sxs-lookup"><span data-stu-id="ecf9a-110">Remove cached information for a team if the bot is removed</span></span>
* <span data-ttu-id="ecf9a-111">Quand un message bot est aimé par un utilisateur</span><span class="sxs-lookup"><span data-stu-id="ecf9a-111">When a bot message is liked by a user</span></span>

<span data-ttu-id="ecf9a-112">Chaque événement bot est envoyé sous la `Activity` forme d’un `messageType` objet qui définit les informations contenues dans l’objet.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="ecf9a-113">Pour les messages de `message`type, consultez la rubrique [envoi et réception de messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span><span class="sxs-lookup"><span data-stu-id="ecf9a-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="ecf9a-114">Les événements teams et Group, généralement déclenchés `conversationUpdate` par le type, ont des informations d’événements teams supplémentaires `channelData` transmises dans le cadre de l’objet et, par `channelData` conséquent, votre gestionnaire `eventType` d’événements doit interroger la charge utile pour les équipes et les métadonnées propres aux événements supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="ecf9a-115">Le tableau suivant répertorie les événements que votre bot peut recevoir et comment agir.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="ecf9a-116">Type</span><span class="sxs-lookup"><span data-stu-id="ecf9a-116">Type</span></span>|<span data-ttu-id="ecf9a-117">Objet Payload</span><span class="sxs-lookup"><span data-stu-id="ecf9a-117">Payload object</span></span>|<span data-ttu-id="ecf9a-118">EventType teams</span><span class="sxs-lookup"><span data-stu-id="ecf9a-118">Teams eventType</span></span> |<span data-ttu-id="ecf9a-119">Description</span><span class="sxs-lookup"><span data-stu-id="ecf9a-119">Description</span></span>|<span data-ttu-id="ecf9a-120">Portée</span><span class="sxs-lookup"><span data-stu-id="ecf9a-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="ecf9a-121">Membre ajouté à Team</span><span class="sxs-lookup"><span data-stu-id="ecf9a-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="ecf9a-122">tous les</span><span class="sxs-lookup"><span data-stu-id="ecf9a-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="ecf9a-123">Le membre a été supprimé de Team</span><span class="sxs-lookup"><span data-stu-id="ecf9a-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="ecf9a-124">L’équipe a été renommée</span><span class="sxs-lookup"><span data-stu-id="ecf9a-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="ecf9a-125">Un canal a été créé</span><span class="sxs-lookup"><span data-stu-id="ecf9a-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="ecf9a-126">Un canal a été renommé.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="ecf9a-127">Un canal a été supprimé</span><span class="sxs-lookup"><span data-stu-id="ecf9a-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="ecf9a-128">Message de réaction au bot</span><span class="sxs-lookup"><span data-stu-id="ecf9a-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="ecf9a-129">tous les</span><span class="sxs-lookup"><span data-stu-id="ecf9a-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="ecf9a-130">Réaction supprimée du message bot</span><span class="sxs-lookup"><span data-stu-id="ecf9a-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="ecf9a-131">tous les</span><span class="sxs-lookup"><span data-stu-id="ecf9a-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="ecf9a-132">Ajout d’un membre d’équipe ou d’un bot</span><span class="sxs-lookup"><span data-stu-id="ecf9a-132">Team member or bot addition</span></span>

<span data-ttu-id="ecf9a-133">L' [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) événement est envoyé à votre bot lorsqu’il reçoit des informations sur les mises à jour d’appartenance de teams dans lesquelles il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="ecf9a-134">Elle reçoit également une mise à jour lorsqu’elle a été ajoutée pour la première fois spécifiquement pour les conversations personnelles.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="ecf9a-135">Notez que les informations utilisateur (`Id`) sont uniques pour votre robot et peuvent être mises en cache pour une utilisation future par votre service (par exemple, l’envoi d’un message à un utilisateur spécifique).</span><span class="sxs-lookup"><span data-stu-id="ecf9a-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="ecf9a-136">Bot ou utilisateur ajouté à une équipe</span><span class="sxs-lookup"><span data-stu-id="ecf9a-136">Bot or user added to a team</span></span>

<span data-ttu-id="ecf9a-137">L' `conversationUpdate` événement dont l' `membersAdded` objet est dans la charge utile est envoyé lorsqu’un bot est ajouté à une équipe ou lorsqu’un nouvel utilisateur est ajouté à une équipe dans laquelle un bot a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="ecf9a-138">Microsoft teams ajoute `eventType.teamMemberAdded` également dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="ecf9a-139">Étant donné que cet événement est envoyé dans les deux cas, vous `membersAdded` devez analyser l’objet pour déterminer si l’ajout était un utilisateur ou le robot lui-même.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="ecf9a-140">Pour ce dernier, il est recommandé d’envoyer un [message de bienvenue](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) à la chaîne afin que les utilisateurs puissent comprendre les fonctionnalités fournies par votre robot.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="ecf9a-141">Exemple de code : vérification du fait que bot était le membre ajouté</span><span class="sxs-lookup"><span data-stu-id="ecf9a-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="ecf9a-142">.NET</span><span class="sxs-lookup"><span data-stu-id="ecf9a-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="ecf9a-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="ecf9a-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="ecf9a-144">Exemple de schéma : Bot ajouté à Team</span><span class="sxs-lookup"><span data-stu-id="ecf9a-144">Schema example: Bot added to team</span></span>

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

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="ecf9a-145">Bot ajouté uniquement pour le contexte personnel</span><span class="sxs-lookup"><span data-stu-id="ecf9a-145">Bot added for personal context only</span></span>

<span data-ttu-id="ecf9a-146">Votre bot reçoit un `conversationUpdate` avec `membersAdded` lorsqu’un utilisateur l’ajoute directement pour la conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-146">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="ecf9a-147">Dans ce cas, la charge utile que reçoit votre bot ne contient `channelData.team` pas l’objet.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-147">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="ecf9a-148">Vous devez l’utiliser comme filtre si vous souhaitez que votre bot propose un autre message d' [Accueil](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) en fonction de l’étendue.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-148">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="ecf9a-149">Pour les robots personnels, votre robot ne recevra jamais l' `conversationUpdate` événement qu’une seule fois, même si le bot est supprimé et rajouté.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-149">For personal scoped bots, your bot will only ever receive the `conversationUpdate` event a single time, even if the bot is removed and re-added.</span></span> <span data-ttu-id="ecf9a-150">Pour le développement et les tests, il peut s’avérer utile d’ajouter une fonction d’assistance qui vous permettra de réinitialiser entièrement votre robot.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-150">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="ecf9a-151">Pour plus d’informations sur l’implémentation de cet exemple, voir un exemple [node. js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) ou [C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) .</span><span class="sxs-lookup"><span data-stu-id="ecf9a-151">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="ecf9a-152">Exemple de schéma : Bot ajouté au contexte personnel</span><span class="sxs-lookup"><span data-stu-id="ecf9a-152">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="ecf9a-153">Membre d’équipe supprimé</span><span class="sxs-lookup"><span data-stu-id="ecf9a-153">Team member or bot removed</span></span>

<span data-ttu-id="ecf9a-154">L' `conversationUpdate` événement dont l' `membersRemoved` objet est dans la charge utile est envoyé lorsque le robot est supprimé d’une équipe ou lorsqu’un utilisateur est supprimé d’une équipe dans laquelle un bot a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-154">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="ecf9a-155">Microsoft teams ajoute `eventType.teamMemberRemoved` également dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-155">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="ecf9a-156">Comme avec l' `membersAdded` objet, vous devez analyser l' `membersRemoved` objet pour identifier l’ID de l’application de votre bot afin de déterminer qui a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-156">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="ecf9a-157">Exemple de schéma : membre d’équipe supprimé</span><span class="sxs-lookup"><span data-stu-id="ecf9a-157">Schema example: Team member removed</span></span>

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

## <a name="team-name-updates"></a><span data-ttu-id="ecf9a-158">Mises à jour de nom d’équipe</span><span class="sxs-lookup"><span data-stu-id="ecf9a-158">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="ecf9a-159">Il n’existe aucune fonctionnalité permettant d’interroger tous les noms d’équipe et le nom de l’équipe n’est pas renvoyé dans les charges par d’autres événements.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-159">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="ecf9a-160">Votre robot est informé de la modification du nom de l’équipe dans laquelle il se trouve.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-160">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="ecf9a-161">Elle reçoit un `conversationUpdate` événement avec `eventType.teamRenamed` dans l' `channelData` objet.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-161">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="ecf9a-162">Veuillez noter qu’il n’existe aucune notification pour la création ou la suppression d’une équipe, car les robots n’existent que dans le cadre de teams et n’ont aucune visibilité en dehors de l’étendue dans laquelle ils ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-162">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="ecf9a-163">Exemple de schéma : équipe renommée</span><span class="sxs-lookup"><span data-stu-id="ecf9a-163">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="ecf9a-164">Mises à jour de canal</span><span class="sxs-lookup"><span data-stu-id="ecf9a-164">Channel updates</span></span>

<span data-ttu-id="ecf9a-165">Votre robot est averti lorsqu’un canal est créé, renommé ou supprimé dans une équipe où il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-165">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="ecf9a-166">Une fois encore `conversationUpdate` , l’événement est reçu et un identificateur d’événement spécifique à teams est envoyé dans le `channelData.eventType` cadre de l’objet, où les `channel.id` données du canal sont le GUID du canal `channel.name` et contient le nom du canal lui-même.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-166">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="ecf9a-167">Les événements de canal sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="ecf9a-167">The channel events are as follows:</span></span>

* <span data-ttu-id="ecf9a-168">**channelCreated**&emsp;un utilisateur ajoute un nouveau canal à l’équipe</span><span class="sxs-lookup"><span data-stu-id="ecf9a-168">**channelCreated**&emsp;A user adds a new channel to the team</span></span>
* <span data-ttu-id="ecf9a-169">**channelRenamed**&emsp;un utilisateur renomme un canal existant</span><span class="sxs-lookup"><span data-stu-id="ecf9a-169">**channelRenamed**&emsp;A user renames an existing channel</span></span>
* <span data-ttu-id="ecf9a-170">**channelDeleted**&emsp;un utilisateur supprime un canal</span><span class="sxs-lookup"><span data-stu-id="ecf9a-170">**channelDeleted**&emsp;A user removes a channel</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="ecf9a-171">Exemple de schéma complet : channelCreated</span><span class="sxs-lookup"><span data-stu-id="ecf9a-171">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="ecf9a-172">Extrait de schéma : channelData pour channelRenamed</span><span class="sxs-lookup"><span data-stu-id="ecf9a-172">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="ecf9a-173">Extrait de schéma : channelData pour channelDeleted</span><span class="sxs-lookup"><span data-stu-id="ecf9a-173">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="ecf9a-174">Réactions</span><span class="sxs-lookup"><span data-stu-id="ecf9a-174">Reactions</span></span>

<span data-ttu-id="ecf9a-175">L' `messageReaction` événement est envoyé lorsqu’un utilisateur ajoute ou supprime sa réaction à un message qui a été envoyé par votre bot.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-175">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="ecf9a-176">`replyToId`contient l’ID du message spécifique.</span><span class="sxs-lookup"><span data-stu-id="ecf9a-176">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="ecf9a-177">Exemple de schéma : un utilisateur aime un message</span><span class="sxs-lookup"><span data-stu-id="ecf9a-177">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="ecf9a-178">Exemple de schéma : un utilisateur n’aime pas un message</span><span class="sxs-lookup"><span data-stu-id="ecf9a-178">Schema example: A user un-likes a message</span></span>

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
