---
title: Gérer les événements bot
description: Décrit comment gérer les événements dans les bots pour Microsoft Teams
keywords: équipes bots événements
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: da624ea0e92e193f4ad7f334d958349d542dd6e0
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566466"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="92fc9-104">Gérer les événements bot dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="92fc9-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="92fc9-105">Microsoft Teams envoie des notifications à votre bot pour les modifications ou les événements qui se produisent dans les étendues où votre bot est actif.</span><span class="sxs-lookup"><span data-stu-id="92fc9-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="92fc9-106">Vous pouvez utiliser ces événements pour déclencher la logique de service, telles que les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="92fc9-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="92fc9-107">Déclenchez un message de bienvenue lorsque votre bot est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="92fc9-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="92fc9-108">Requête et cache d’informations de groupe lorsque le bot est ajouté à un chat de groupe.</span><span class="sxs-lookup"><span data-stu-id="92fc9-108">Query and cache group information when the bot is added to a group chat.</span></span>
* <span data-ttu-id="92fc9-109">Mettre à jour les informations mises en cache sur l’adhésion à l’équipe ou les informations de canal.</span><span class="sxs-lookup"><span data-stu-id="92fc9-109">Update cached information on team membership or channel information.</span></span>
* <span data-ttu-id="92fc9-110">Supprimez les informations mises en cache pour une équipe si le bot est supprimé.</span><span class="sxs-lookup"><span data-stu-id="92fc9-110">Remove cached information for a team if the bot is removed.</span></span>
* <span data-ttu-id="92fc9-111">Lorsqu’un message bot est aimé par un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="92fc9-111">When a bot message is liked by a user.</span></span>

<span data-ttu-id="92fc9-112">Chaque événement bot est envoyé comme un `Activity` objet dans lequel définit quelles informations sont dans `messageType` l’objet.</span><span class="sxs-lookup"><span data-stu-id="92fc9-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="92fc9-113">Pour les messages de type `message` , voir Envoi et réception de [messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span><span class="sxs-lookup"><span data-stu-id="92fc9-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="92fc9-114">Teams et les événements de groupe, généralement déclenchés hors `conversationUpdate` du type, ont des informations d’événement Teams supplémentaires transmises dans le cadre `channelData` de l’objet, et donc votre gestionnaire d’événements doit interroger la `channelData` charge utile pour les Teams et les `eventType` métadonnées supplémentaires spécifiques à l’événement.</span><span class="sxs-lookup"><span data-stu-id="92fc9-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="92fc9-115">Le tableau suivant énumère les événements que votre bot peut recevoir et prendre des mesures.</span><span class="sxs-lookup"><span data-stu-id="92fc9-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="92fc9-116">Type</span><span class="sxs-lookup"><span data-stu-id="92fc9-116">Type</span></span>|<span data-ttu-id="92fc9-117">Objet de charge utile</span><span class="sxs-lookup"><span data-stu-id="92fc9-117">Payload object</span></span>|<span data-ttu-id="92fc9-118">Teams événementType</span><span class="sxs-lookup"><span data-stu-id="92fc9-118">Teams eventType</span></span> |<span data-ttu-id="92fc9-119">Description</span><span class="sxs-lookup"><span data-stu-id="92fc9-119">Description</span></span>|<span data-ttu-id="92fc9-120">Portée</span><span class="sxs-lookup"><span data-stu-id="92fc9-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="92fc9-121">Membre ajouté à l’équipe</span><span class="sxs-lookup"><span data-stu-id="92fc9-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="92fc9-122">tout</span><span class="sxs-lookup"><span data-stu-id="92fc9-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="92fc9-123">Membre a été retiré de l’équipe</span><span class="sxs-lookup"><span data-stu-id="92fc9-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="92fc9-124">L’équipe a été rebaptisée</span><span class="sxs-lookup"><span data-stu-id="92fc9-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="92fc9-125">Un canal a été créé</span><span class="sxs-lookup"><span data-stu-id="92fc9-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="92fc9-126">Une chaîne a été rebaptisée</span><span class="sxs-lookup"><span data-stu-id="92fc9-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="92fc9-127">Un canal a été supprimé</span><span class="sxs-lookup"><span data-stu-id="92fc9-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="92fc9-128">Réaction au message bot</span><span class="sxs-lookup"><span data-stu-id="92fc9-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="92fc9-129">tout</span><span class="sxs-lookup"><span data-stu-id="92fc9-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="92fc9-130">Réaction supprimée du message bot</span><span class="sxs-lookup"><span data-stu-id="92fc9-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="92fc9-131">tout</span><span class="sxs-lookup"><span data-stu-id="92fc9-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="92fc9-132">Membre de l’équipe ou ajout de bot</span><span class="sxs-lookup"><span data-stu-id="92fc9-132">Team member or bot addition</span></span>

<span data-ttu-id="92fc9-133">[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true)L’événement est envoyé à votre bot lorsqu’il reçoit des informations sur les mises à jour des membres pour les équipes où il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="92fc9-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="92fc9-134">Il reçoit également une mise à jour lorsqu’il a été ajouté pour la première fois, spécifiquement pour les conversations personnelles.</span><span class="sxs-lookup"><span data-stu-id="92fc9-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="92fc9-135">Notez que les informations utilisateur ( `Id` ) est unique pour votre bot et peut être mis en cache pour une utilisation future par votre service, comme, l’envoi d’un message à un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="92fc9-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service, such as, sending a message to a specific user.</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="92fc9-136">Bot ou utilisateur ajouté à une équipe</span><span class="sxs-lookup"><span data-stu-id="92fc9-136">Bot or user added to a team</span></span>

<span data-ttu-id="92fc9-137">`conversationUpdate`L’événement avec `membersAdded` l’objet dans la charge utile est envoyé lorsqu’un bot est ajouté à une équipe ou qu’un nouvel utilisateur est ajouté à une équipe où un bot a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="92fc9-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="92fc9-138">Microsoft Teams ajoute également `eventType.teamMemberAdded` dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="92fc9-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="92fc9-139">Étant donné que cet événement est envoyé dans les deux cas, vous devez examiner `membersAdded` l’objet pour déterminer si l’ajout était un utilisateur ou le bot lui-même.</span><span class="sxs-lookup"><span data-stu-id="92fc9-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="92fc9-140">Pour ce dernier, une bonne pratique est d’envoyer un [message de bienvenue au](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) canal afin que les utilisateurs puissent comprendre les fonctionnalités de votre bot fournit.</span><span class="sxs-lookup"><span data-stu-id="92fc9-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="92fc9-141">Exemple de code : Vérifier si bot était le membre ajouté</span><span class="sxs-lookup"><span data-stu-id="92fc9-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="92fc9-142">.NET</span><span class="sxs-lookup"><span data-stu-id="92fc9-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="92fc9-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="92fc9-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="92fc9-144">Exemple de schéma : Bot ajouté à l’équipe</span><span class="sxs-lookup"><span data-stu-id="92fc9-144">Schema example: Bot added to team</span></span>

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a><span data-ttu-id="92fc9-145">Utilisateur ajouté à une réunion</span><span class="sxs-lookup"><span data-stu-id="92fc9-145">User Added to a meeting</span></span>

<span data-ttu-id="92fc9-146">`conversationUpdate`L’événement avec `membersAdded` l’objet dans la charge utile est envoyé lorsqu’un utilisateur est ajouté à une réunion privée planifiée.</span><span class="sxs-lookup"><span data-stu-id="92fc9-146">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when a user is added to a private scheduled meeting.</span></span> <span data-ttu-id="92fc9-147">Les détails de l’événement seront envoyés même lorsque des utilisateurs anonymes se joindront à la réunion.</span><span class="sxs-lookup"><span data-stu-id="92fc9-147">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="92fc9-148">Lorsqu’un utilisateur anonyme est ajouté à une réunion, l’objet de charge utile membersAdded n’a pas de `aadObjectId` champ.</span><span class="sxs-lookup"><span data-stu-id="92fc9-148">When an anonymous user is added to a meeting, membersAdded payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="92fc9-149">Lorsqu’un utilisateur anonyme est ajouté à une réunion, `from` l’objet de la charge utile a toujours l’id de l’organisateur de la réunion, même si l’utilisateur anonyme a été ajouté par un autre présentateur.</span><span class="sxs-lookup"><span data-stu-id="92fc9-149">When an anonymous user is added to a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was added by another presenter.</span></span>

#### <a name="schema-example-user-added-to-meeting"></a><span data-ttu-id="92fc9-150">Exemple de schéma : Utilisateur ajouté à la réunion</span><span class="sxs-lookup"><span data-stu-id="92fc9-150">Schema example: User added to meeting</span></span>

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="92fc9-151">Bot ajouté pour le contexte personnel seulement</span><span class="sxs-lookup"><span data-stu-id="92fc9-151">Bot added for personal context only</span></span>

<span data-ttu-id="92fc9-152">Votre bot reçoit un `conversationUpdate` avec quand un utilisateur `membersAdded` l’ajoute directement pour le chat personnel.</span><span class="sxs-lookup"><span data-stu-id="92fc9-152">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="92fc9-153">Dans ce cas, la charge utile que votre bot reçoit ne contient pas `channelData.team` l’objet.</span><span class="sxs-lookup"><span data-stu-id="92fc9-153">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="92fc9-154">Vous devez l’utiliser comme filtre au cas où vous souhaitez que votre bot offre un message de [bienvenue différent en fonction](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) de la portée.</span><span class="sxs-lookup"><span data-stu-id="92fc9-154">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="92fc9-155">Pour les bots personnels, votre bot recevra `conversationUpdate` l’événement plusieurs fois, même si le bot est supprimé et ré-ajouté.</span><span class="sxs-lookup"><span data-stu-id="92fc9-155">For personal scoped bots, your bot will  receive the `conversationUpdate` event multiple times, even if the bot is removed and re-added.</span></span> <span data-ttu-id="92fc9-156">Pour le développement et les tests, vous trouverez peut-être utile d’ajouter une fonction d’aide qui vous permettra de réinitialiser complètement votre bot.</span><span class="sxs-lookup"><span data-stu-id="92fc9-156">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="92fc9-157">Voir un exemple [Node.js C# pour](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) [plus de détails sur la](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) mise en œuvre de cette.</span><span class="sxs-lookup"><span data-stu-id="92fc9-157">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="92fc9-158">Exemple de schéma : bot ajouté au contexte personnel</span><span class="sxs-lookup"><span data-stu-id="92fc9-158">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="92fc9-159">Membre de l’équipe ou bot retiré</span><span class="sxs-lookup"><span data-stu-id="92fc9-159">Team member or bot removed</span></span>

<span data-ttu-id="92fc9-160">`conversationUpdate`L’événement avec `membersRemoved` l’objet dans la charge utile est envoyé lorsque votre bot est retiré d’une équipe, ou qu’un utilisateur est retiré d’une équipe où un bot a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="92fc9-160">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="92fc9-161">Microsoft Teams ajoute également `eventType.teamMemberRemoved` dans `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="92fc9-161">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="92fc9-162">Comme pour `membersAdded` l’objet, vous devez parse `membersRemoved` l’objet de l’ID app de votre bot pour déterminer qui a été supprimé.</span><span class="sxs-lookup"><span data-stu-id="92fc9-162">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="92fc9-163">Exemple de schéma : Membre de l’équipe supprimé</span><span class="sxs-lookup"><span data-stu-id="92fc9-163">Schema example: Team member removed</span></span>

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

### <a name="user-removed-from-a-meeting"></a><span data-ttu-id="92fc9-164">Utilisateur retiré d’une réunion</span><span class="sxs-lookup"><span data-stu-id="92fc9-164">User removed from a meeting</span></span>

<span data-ttu-id="92fc9-165">`conversationUpdate`L’événement avec `membersRemoved` l’objet dans la charge utile est envoyé lorsqu’un utilisateur est retiré d’une réunion planifiée privée.</span><span class="sxs-lookup"><span data-stu-id="92fc9-165">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when a user is removed from a private scheduled meeting.</span></span> <span data-ttu-id="92fc9-166">Les détails de l’événement seront envoyés même lorsque des utilisateurs anonymes se joindront à la réunion.</span><span class="sxs-lookup"><span data-stu-id="92fc9-166">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="92fc9-167">Lorsqu’un utilisateur anonyme est retiré d’une réunion, l’objet de charge utile de membersRemoved n’a pas `aadObjectId` de champ.</span><span class="sxs-lookup"><span data-stu-id="92fc9-167">When an anonymous user is removed from a meeting, membersRemoved payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="92fc9-168">Lorsqu’un utilisateur anonyme est retiré d’une réunion, `from` l’objet de la charge utile a toujours l’id de l’organisateur de la réunion, même si l’utilisateur anonyme a été supprimé par un autre présentateur.</span><span class="sxs-lookup"><span data-stu-id="92fc9-168">When an anonymous user is removed from a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was removed by another presenter.</span></span>

#### <a name="schema-example-user-removed-from-meeting"></a><span data-ttu-id="92fc9-169">Exemple de schéma : Utilisateur retiré de la réunion</span><span class="sxs-lookup"><span data-stu-id="92fc9-169">Schema example: User removed from meeting</span></span>

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a><span data-ttu-id="92fc9-170">Mises à jour des noms d’équipe</span><span class="sxs-lookup"><span data-stu-id="92fc9-170">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="92fc9-171">Il n’y a aucune fonctionnalité pour interroger tous les noms d’équipe, et le nom de l’équipe n’est pas retourné dans les charges utiles d’autres événements.</span><span class="sxs-lookup"><span data-stu-id="92fc9-171">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="92fc9-172">Votre bot est notifié lorsque l’équipe dans qui il se trouve a été rebaptisée.</span><span class="sxs-lookup"><span data-stu-id="92fc9-172">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="92fc9-173">Il reçoit un `conversationUpdate` événement avec dans `eventType.teamRenamed` `channelData` l’objet.</span><span class="sxs-lookup"><span data-stu-id="92fc9-173">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="92fc9-174">Veuillez noter qu’il n’y a pas de notifications pour la création ou la suppression d’équipes, car les bots n’existent que dans le cadre d’équipes et n’ont aucune visibilité en dehors du champ d’application dans lequel ils ont été ajoutés.</span><span class="sxs-lookup"><span data-stu-id="92fc9-174">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="92fc9-175">Exemple de schéma : Équipe renommée</span><span class="sxs-lookup"><span data-stu-id="92fc9-175">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="92fc9-176">Mises à jour des canaux</span><span class="sxs-lookup"><span data-stu-id="92fc9-176">Channel updates</span></span>

<span data-ttu-id="92fc9-177">Votre bot est notifié lorsqu’un canal est créé, renommé ou supprimé dans une équipe où il a été ajouté.</span><span class="sxs-lookup"><span data-stu-id="92fc9-177">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="92fc9-178">Encore une fois, `conversationUpdate` l’événement est reçu, et un identificateur d’événement spécifique à Teams est envoyé dans le cadre de `channelData.eventType` l’objet, où les données du canal est le GUID pour le `channel.id` canal, et `channel.name` contient le nom du canal lui-même.</span><span class="sxs-lookup"><span data-stu-id="92fc9-178">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="92fc9-179">Les événements de la chaîne sont les suivants:</span><span class="sxs-lookup"><span data-stu-id="92fc9-179">The channel events are as follows:</span></span>

* <span data-ttu-id="92fc9-180">**canalCréé** &emsp; Un utilisateur ajoute un nouveau canal à l’équipe.</span><span class="sxs-lookup"><span data-stu-id="92fc9-180">**channelCreated**&emsp;A user adds a new channel to the team.</span></span>
* <span data-ttu-id="92fc9-181">**canalRenamed** &emsp; Un utilisateur renomme un canal existant.</span><span class="sxs-lookup"><span data-stu-id="92fc9-181">**channelRenamed**&emsp;A user renames an existing channel.</span></span>
* <span data-ttu-id="92fc9-182">**canalDeleted** &emsp; Un utilisateur supprime un canal.</span><span class="sxs-lookup"><span data-stu-id="92fc9-182">**channelDeleted**&emsp;A user removes a channel.</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="92fc9-183">Exemple complet de schéma : canalCréé</span><span class="sxs-lookup"><span data-stu-id="92fc9-183">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="92fc9-184">Extrait de Schema: channelData pour channelRenamed</span><span class="sxs-lookup"><span data-stu-id="92fc9-184">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="92fc9-185">Extrait de Schema: channelData pour channelDeleted</span><span class="sxs-lookup"><span data-stu-id="92fc9-185">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="92fc9-186">Réactions</span><span class="sxs-lookup"><span data-stu-id="92fc9-186">Reactions</span></span>

<span data-ttu-id="92fc9-187">`messageReaction`L’événement est envoyé lorsqu’un utilisateur ajoute ou supprime sa réaction à un message qui a été envoyé à l’origine par votre bot.</span><span class="sxs-lookup"><span data-stu-id="92fc9-187">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="92fc9-188">`replyToId` contient l’ID du message spécifique.</span><span class="sxs-lookup"><span data-stu-id="92fc9-188">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="92fc9-189">Exemple de schéma : Un utilisateur aime un message</span><span class="sxs-lookup"><span data-stu-id="92fc9-189">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="92fc9-190">Exemple de schéma : un utilisateur n’aime pas un message</span><span class="sxs-lookup"><span data-stu-id="92fc9-190">Schema example: A user un-likes a message</span></span>

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
