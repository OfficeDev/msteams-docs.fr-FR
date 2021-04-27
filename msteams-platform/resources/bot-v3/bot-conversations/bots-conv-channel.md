---
title: Conversations de conversation de canal et de groupe avec des bots
description: Décrit le scénario de bout en bout d'une conversation avec un bot dans un canal dans Microsoft Teams
keywords: teams scenarios channels conversation bot
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: 2eac067a75fc75c9991e8b30ec5d693d89ed8228
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019796"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="8303c-104">Conversations par chat de canal et de groupe avec un robot Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8303c-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="8303c-105">Microsoft Teams permet aux utilisateurs d'amener des bots dans leurs conversations de canal ou de groupe.</span><span class="sxs-lookup"><span data-stu-id="8303c-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="8303c-106">En ajoutant un bot à une équipe ou à une conversation, tous les utilisateurs de la conversation peuvent tirer parti des fonctionnalités du bot directement dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="8303c-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="8303c-107">Vous pouvez également accéder aux fonctionnalités propres à Teams au sein de votre bot, telles que l'interrogation d'informations d'équipe et @mentioning utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8303c-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="8303c-108">La conversation dans les canaux et les conversations de groupe diffère de la conversation personnelle, dans la fait que l'utilisateur doit @mention le bot.</span><span class="sxs-lookup"><span data-stu-id="8303c-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="8303c-109">Si un bot est utilisé dans plusieurs étendues (personnelles, groupchat ou canal), vous devez détecter l'étendue d'où les messages du bot sont issus et les traiter en conséquence.</span><span class="sxs-lookup"><span data-stu-id="8303c-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="8303c-110">Conception d'un bot idéal pour les canaux ou les groupes</span><span class="sxs-lookup"><span data-stu-id="8303c-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="8303c-111">Les bots ajoutés à une équipe deviennent un autre membre de l'équipe et peuvent être @mentioned dans le cadre de la conversation.</span><span class="sxs-lookup"><span data-stu-id="8303c-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="8303c-112">En fait, les bots reçoivent des messages uniquement lorsqu'ils @mentioned, de sorte que les autres conversations sur le canal ne sont pas envoyées au bot.</span><span class="sxs-lookup"><span data-stu-id="8303c-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="8303c-113">Un bot dans un groupe ou un canal doit fournir des informations pertinentes et appropriées pour tous les membres.</span><span class="sxs-lookup"><span data-stu-id="8303c-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="8303c-114">Bien que votre bot puisse certainement fournir des informations pertinentes pour l'expérience, gardez à l'esprit que les conversations avec elle sont visibles par tout le monde.</span><span class="sxs-lookup"><span data-stu-id="8303c-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="8303c-115">Par conséquent, un bot efficace dans un groupe ou un canal doit ajouter de la valeur à tous les utilisateurs et ne pas partager par inadvertance des informations plus appropriées à une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="8303c-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="8303c-116">Votre bot, comme il est, peut être entièrement pertinent dans toutes les étendues sans nécessiter de travail supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="8303c-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="8303c-117">Dans Microsoft Teams, il n'est pas attendu que votre bot fonctionne dans toutes les étendues, mais vous devez vous assurer que votre bot fournit une valeur utilisateur dans n'importe quelle étendue que vous choisissez de prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="8303c-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="8303c-118">Pour plus d'informations sur les étendues, voir [Applications dans Microsoft Teams.](~/concepts/build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="8303c-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="8303c-119">Le développement d'un bot qui fonctionne dans des groupes ou des canaux utilise la plupart des mêmes fonctionnalités que les conversations personnelles.</span><span class="sxs-lookup"><span data-stu-id="8303c-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="8303c-120">Des événements et des données supplémentaires dans la charge utile fournissent des informations de groupe et de canal Teams.</span><span class="sxs-lookup"><span data-stu-id="8303c-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="8303c-121">Ces différences, ainsi que les principales différences de fonctionnalités courantes, sont décrites dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="8303c-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="8303c-122">Création de messages</span><span class="sxs-lookup"><span data-stu-id="8303c-122">Creating messages</span></span>

<span data-ttu-id="8303c-123">Pour plus d'informations sur les bots qui créent des messages dans les canaux, voir Messagerie proactive pour les [bots,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)et plus spécifiquement Création [d'une conversation de canal.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)</span><span class="sxs-lookup"><span data-stu-id="8303c-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="8303c-124">Réception de messages</span><span class="sxs-lookup"><span data-stu-id="8303c-124">Receiving messages</span></span>

<span data-ttu-id="8303c-125">Pour un bot dans un groupe ou un canal, en plus du schéma de [message](https://docs.botframework.com/core-concepts/reference/#activity)normal, votre bot reçoit également les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="8303c-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="8303c-126">`channelData`Voir [les données du canal Teams.](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)</span><span class="sxs-lookup"><span data-stu-id="8303c-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="8303c-127">Dans une conversation de groupe, contient des informations spécifiques à cette conversation.</span><span class="sxs-lookup"><span data-stu-id="8303c-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="8303c-128">`conversation.id` ID de chaîne de réponse, constitué de l'ID de canal et de l'ID du premier message de la chaîne de réponse</span><span class="sxs-lookup"><span data-stu-id="8303c-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="8303c-129">`conversation.isGroup` Est pour `true` les messages de bot dans les canaux ou les conversations de groupe</span><span class="sxs-lookup"><span data-stu-id="8303c-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="8303c-130">`conversation.conversationType``groupChat`L'une ou l'autre ou`channel`</span><span class="sxs-lookup"><span data-stu-id="8303c-130">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="8303c-131">`entities` Peut contenir une ou plusieurs mentions (voir [Mentions](#-mentions))</span><span class="sxs-lookup"><span data-stu-id="8303c-131">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="8303c-132">Réponse aux messages</span><span class="sxs-lookup"><span data-stu-id="8303c-132">Replying to messages</span></span>

<span data-ttu-id="8303c-133">Pour répondre à un message existant, [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) appelez .NET ou [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) dans Node.js.</span><span class="sxs-lookup"><span data-stu-id="8303c-133">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="8303c-134">Le SDK Bot Builder gère tous les détails.</span><span class="sxs-lookup"><span data-stu-id="8303c-134">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="8303c-135">Si vous choisissez d'utiliser l'API REST, vous pouvez également appeler le [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8303c-135">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="8303c-136">Dans un canal, la réponse à un message s'affiche comme une réponse à la chaîne de réponse à l'origine.</span><span class="sxs-lookup"><span data-stu-id="8303c-136">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="8303c-137">Contient `conversation.id` le canal et l'ID de message de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="8303c-137">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="8303c-138">Bien que Bot Framework s'occupe des détails, vous pouvez le mettre en cache pour les réponses ultérieures à ce `conversation.id` thread de conversation si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="8303c-138">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="8303c-139">Meilleure pratique : messages de bienvenue dans Teams</span><span class="sxs-lookup"><span data-stu-id="8303c-139">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="8303c-140">Lorsque votre bot est ajouté pour la première fois au groupe ou à l'équipe, il est généralement utile d'envoyer un message de bienvenue présentant le bot à tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8303c-140">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="8303c-141">Le message de bienvenue doit fournir une description des fonctionnalités et des avantages du bot pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="8303c-141">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="8303c-142">Dans l'idéal, le message doit également inclure des commandes pour permettre à l'utilisateur d'interagir avec l'application.</span><span class="sxs-lookup"><span data-stu-id="8303c-142">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="8303c-143">Pour ce faire, assurez-vous que votre bot répond au message, avec `conversationUpdate` `teamsAddMembers` l'eventType dans `channelData` l'objet.</span><span class="sxs-lookup"><span data-stu-id="8303c-143">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="8303c-144">Assurez-vous que l'ID est lui-même l'ID d'application du bot, car le même événement est envoyé lorsqu'un utilisateur est ajouté `memberAdded` à une équipe.</span><span class="sxs-lookup"><span data-stu-id="8303c-144">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="8303c-145">Pour plus [d'informations, voir l'ajout](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) d'un membre d'équipe ou d'un bot.</span><span class="sxs-lookup"><span data-stu-id="8303c-145">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="8303c-146">Vous pouvez également envoyer un message personnel à chaque membre de l'équipe lorsque le bot est ajouté.</span><span class="sxs-lookup"><span data-stu-id="8303c-146">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="8303c-147">Pour ce faire, vous pouvez récupérer [la liste](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) de l'équipe et envoyer un message direct à [chaque utilisateur.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="8303c-147">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="8303c-148">Il est recommandé que votre bot *n'envoie* pas de message de bienvenue dans les situations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8303c-148">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="8303c-149">L'équipe est volumineuse (évidemment subjectif, mais par exemple plus de 100 membres).</span><span class="sxs-lookup"><span data-stu-id="8303c-149">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="8303c-150">Votre bot peut être considéré comme « spammy » et la personne qui l'a ajouté peut obtenir des réclamations, sauf si vous communiquez clairement la proposition de valeur de votre bot à toutes les personnes qui voient le message de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="8303c-150">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="8303c-151">Votre bot est d'abord mentionné dans un groupe ou un canal (plutôt que d'être ajouté pour la première fois à une équipe)</span><span class="sxs-lookup"><span data-stu-id="8303c-151">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="8303c-152">Un groupe ou un canal est renommé</span><span class="sxs-lookup"><span data-stu-id="8303c-152">A group or channel is renamed</span></span>
* <span data-ttu-id="8303c-153">Un membre d'équipe est ajouté à un groupe ou un canal</span><span class="sxs-lookup"><span data-stu-id="8303c-153">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="8303c-154">@ Mentions</span><span class="sxs-lookup"><span data-stu-id="8303c-154">@ Mentions</span></span>

<span data-ttu-id="8303c-155">Étant donné que les bots d'un groupe ou d'un canal répondent uniquement lorsqu'ils sont mentionnés (« @_botname_») dans un message, chaque message reçu par un bot dans un canal de groupe contient son propre nom, et vous devez vous assurer que votre message est traité par l'ensemble des messages.</span><span class="sxs-lookup"><span data-stu-id="8303c-155">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="8303c-156">En outre, les bots peuvent passer en détail les autres utilisateurs mentionnés et mentionner des utilisateurs dans le cadre de leurs messages.</span><span class="sxs-lookup"><span data-stu-id="8303c-156">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="8303c-157">Récupération des mentions</span><span class="sxs-lookup"><span data-stu-id="8303c-157">Retrieving mentions</span></span>

<span data-ttu-id="8303c-158">Les mentions sont renvoyées dans l'objet dans la charge utile et contiennent l'ID unique de l'utilisateur et, dans la plupart des cas, le nom de `entities` l'utilisateur mentionné.</span><span class="sxs-lookup"><span data-stu-id="8303c-158">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="8303c-159">Vous pouvez récupérer toutes les mentions dans le message en appelant la fonction dans le SDK Bot Builder pour .NET, qui renvoie un tableau `GetMentions` `Mentioned` d'objets.</span><span class="sxs-lookup"><span data-stu-id="8303c-159">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="8303c-160">Exemple de code .NET : vérifier et @bot mention</span><span class="sxs-lookup"><span data-stu-id="8303c-160">.NET example code: Check for and strip @bot mention</span></span>

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> <span data-ttu-id="8303c-161">Vous pouvez également utiliser la fonction d'extension Teams, qui permet d'enlever toutes les `GetTextWithoutMentions` mentions, y compris le bot.</span><span class="sxs-lookup"><span data-stu-id="8303c-161">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="8303c-162">Node.js exemple de code : Vérifier et @bot mention</span><span class="sxs-lookup"><span data-stu-id="8303c-162">Node.js example code: Check for and strip @bot mention</span></span>

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

<span data-ttu-id="8303c-163">Vous pouvez également utiliser la fonction d'extension Teams, qui permet d'rallonger toutes `getTextWithoutMentions` les mentions, y compris le bot.</span><span class="sxs-lookup"><span data-stu-id="8303c-163">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="8303c-164">Construction de mentions</span><span class="sxs-lookup"><span data-stu-id="8303c-164">Constructing mentions</span></span>

<span data-ttu-id="8303c-165">Votre bot peut mentionner d'autres utilisateurs dans les messages publiés dans les canaux.</span><span class="sxs-lookup"><span data-stu-id="8303c-165">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="8303c-166">Pour ce faire, votre message doit :</span><span class="sxs-lookup"><span data-stu-id="8303c-166">To do this, your message must do the following:</span></span>

* <span data-ttu-id="8303c-167">Inclure `<at>@username</at>` dans le texte du message</span><span class="sxs-lookup"><span data-stu-id="8303c-167">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="8303c-168">Inclure `mention` l'objet à l'intérieur de la collection entities</span><span class="sxs-lookup"><span data-stu-id="8303c-168">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="8303c-169">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="8303c-169">.NET example</span></span>

<span data-ttu-id="8303c-170">Cet exemple utilise le package [NuGet Microsoft.Bot.Connector.Teams.](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)</span><span class="sxs-lookup"><span data-stu-id="8303c-170">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="8303c-171">Node.js exemple</span><span class="sxs-lookup"><span data-stu-id="8303c-171">Node.js example</span></span>

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="8303c-172">Exemple : Message sortant avec l'utilisateur mentionné</span><span class="sxs-lookup"><span data-stu-id="8303c-172">Example: Outgoing message with user mentioned</span></span>

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="8303c-173">Accès à l'étendue groupChat ou canal</span><span class="sxs-lookup"><span data-stu-id="8303c-173">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="8303c-174">Votre bot peut faire plus que d'envoyer et de recevoir des messages dans des groupes et des équipes.</span><span class="sxs-lookup"><span data-stu-id="8303c-174">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="8303c-175">Par exemple, il peut également récupérer la liste des membres, y compris leurs informations de profil, ainsi que la liste des canaux.</span><span class="sxs-lookup"><span data-stu-id="8303c-175">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="8303c-176">Pour [en savoir plus, consultez](~/resources/bot-v3/bots-context.md) Obtenir le contexte de votre bot Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8303c-176">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="8303c-177">*Voir aussi des* [exemples Bot Framework.](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)</span><span class="sxs-lookup"><span data-stu-id="8303c-177">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
