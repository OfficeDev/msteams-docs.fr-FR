---
title: Conversations de conversation de groupe et de canal avec les robots
description: Décrit le scénario de bout en bout d’une conversation avec un bot dans un canal dans Microsoft teams
keywords: scénarios teams-robots de conversation des canaux
ms.date: 06/25/2019
ms.openlocfilehash: 168abd1e3894b95983eec01541d470f1b5384a66
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673591"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="48761-104">Conversations de conversation de groupe et de canal avec un robot Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="48761-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="48761-105">Microsoft teams permet aux utilisateurs d’amener des robots à leurs conversations de conversation de groupe ou de canal.</span><span class="sxs-lookup"><span data-stu-id="48761-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="48761-106">En ajoutant un bot à une équipe ou une conversation, tous les utilisateurs de la conversation peuvent tirer parti de la fonctionnalité de robot directement dans la conversation.</span><span class="sxs-lookup"><span data-stu-id="48761-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="48761-107">Vous pouvez également accéder aux fonctionnalités propres à teams dans votre bot, telles que l’interrogation des informations d’équipe et des utilisateurs de @mentioning.</span><span class="sxs-lookup"><span data-stu-id="48761-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="48761-108">La conversation dans les canaux et les conversations de groupe diffèrent de la conversation personnelle en ce que l’utilisateur doit @mention le bot.</span><span class="sxs-lookup"><span data-stu-id="48761-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="48761-109">Si un bot est utilisé dans plusieurs étendues (personnel, groupchat ou canal), vous devez détecter l’étendue d’origine des messages du bot et les traiter en conséquence.</span><span class="sxs-lookup"><span data-stu-id="48761-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="48761-110">Conception d’un robot idéal pour les canaux ou les groupes</span><span class="sxs-lookup"><span data-stu-id="48761-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="48761-111">Les robots ajoutés à une équipe deviennent un autre membre de l’équipe, qui peut être @mentioned dans le cadre de la conversation.</span><span class="sxs-lookup"><span data-stu-id="48761-111">Bots added to a team become another team member, who can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="48761-112">En fait, les robots reçoivent uniquement les messages lorsqu’ils sont @mentioned, de sorte que les autres conversations sur le canal ne sont pas envoyées au bot.</span><span class="sxs-lookup"><span data-stu-id="48761-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="48761-113">Pour plus de commodité lors de la réponse à des messages de bot dans un canal, le nom du bot est automatiquement ajouté à la zone composer un message.</span><span class="sxs-lookup"><span data-stu-id="48761-113">For convenience when replying to bot messages in a channel, the bot name is prepended in the compose message box automatically.</span></span>

<span data-ttu-id="48761-114">Un bot d’un groupe ou d’un canal doit fournir des informations pertinentes et appropriées pour tous les membres.</span><span class="sxs-lookup"><span data-stu-id="48761-114">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="48761-115">Si votre robot peut certainement fournir des informations pertinentes pour l’expérience, gardez à l’esprit que les conversations sont visibles par tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="48761-115">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="48761-116">Par conséquent, un bon robot d’un groupe ou d’un canal doit ajouter de la valeur à tous les utilisateurs et ne pas partager par inadvertance les informations de façon plus appropriée dans une conversation un-à-un.</span><span class="sxs-lookup"><span data-stu-id="48761-116">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate in a one-to-one conversation.</span></span>

<span data-ttu-id="48761-117">Votre robot peut être entièrement pertinent dans toutes les étendues telles quelles et aucun travail supplémentaire significatif n’est nécessaire pour permettre à votre robot de travailler dessus.</span><span class="sxs-lookup"><span data-stu-id="48761-117">Your bot might be entirely relevant in all scopes as is, and no significant extra work is required to allow your bot to work across them.</span></span> <span data-ttu-id="48761-118">Dans Microsoft Teams, il n’y a aucune attente que votre bot fonctionne dans toutes les étendues, mais vous devez vous assurer que votre robot fournit la valeur de l’utilisateur dans n’importe quelle étendue que vous choisissez de prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="48761-118">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="48761-119">Pour plus d’informations sur les étendues, consultez la rubrique [applications dans Microsoft teams](~/concepts/build-and-test/app-studio-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48761-119">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="48761-120">Le développement d’un bot qui fonctionne dans des groupes ou des canaux utilise la plupart des fonctionnalités des conversations personnelles.</span><span class="sxs-lookup"><span data-stu-id="48761-120">Developing a bot that works in groups or channels uses much of the same functionality from personal conversations.</span></span> <span data-ttu-id="48761-121">Les autres événements et données de la charge utile fournissent des informations sur le groupe teams et le canal.</span><span class="sxs-lookup"><span data-stu-id="48761-121">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="48761-122">Ces différences, ainsi que les principales différences entre les fonctionnalités communes, sont décrites dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="48761-122">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="48761-123">Création de messages</span><span class="sxs-lookup"><span data-stu-id="48761-123">Creating messages</span></span>

<span data-ttu-id="48761-124">Pour plus d’informations sur les robots de création de messages dans les canaux, consultez la rubrique [messagerie proactive pour les robots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)et [création d’une conversation de canal](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span><span class="sxs-lookup"><span data-stu-id="48761-124">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="48761-125">Réception de messages</span><span class="sxs-lookup"><span data-stu-id="48761-125">Receiving messages</span></span>

<span data-ttu-id="48761-126">Pour un bot d’un groupe ou d’un canal, outre le [schéma de message normal](https://docs.botframework.com/core-concepts/reference/#activity), votre bot reçoit également les propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="48761-126">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="48761-127">`channelData`Voir [teams Channel Data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span><span class="sxs-lookup"><span data-stu-id="48761-127">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="48761-128">Dans une conversation de groupe, contient des informations spécifiques à cette conversation.</span><span class="sxs-lookup"><span data-stu-id="48761-128">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="48761-129">`conversation.id`ID de la chaîne de réponse, composé de l’ID du canal plus l’ID du premier message de la chaîne de réponse.</span><span class="sxs-lookup"><span data-stu-id="48761-129">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="48761-130">`conversation.isGroup`Est `true` destiné aux messages bot dans les canaux ou les conversations de groupe</span><span class="sxs-lookup"><span data-stu-id="48761-130">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="48761-131">`conversation.conversationType`Soit `groupChat` ou`channel`</span><span class="sxs-lookup"><span data-stu-id="48761-131">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="48761-132">`entities`Peut contenir une ou plusieurs mentions (voir [mentions](#-mentions))</span><span class="sxs-lookup"><span data-stu-id="48761-132">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="48761-133">Réponse aux messages</span><span class="sxs-lookup"><span data-stu-id="48761-133">Replying to messages</span></span>

<span data-ttu-id="48761-134">Pour répondre à un message existant, appelez [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) le .net ou [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) dans node. js.</span><span class="sxs-lookup"><span data-stu-id="48761-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="48761-135">Le kit de développement logiciel (SDK) du générateur de robots gère tous les détails.</span><span class="sxs-lookup"><span data-stu-id="48761-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="48761-136">Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="48761-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="48761-137">Dans un canal, la réponse à un message apparaît sous la forme d’une réponse à la chaîne de réponse initiale.</span><span class="sxs-lookup"><span data-stu-id="48761-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="48761-138">Le `conversation.id` contient le canal et l’ID de message de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="48761-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="48761-139">Bien que l’infrastructure de bot prenne en charge les détails, vous `conversation.id` pouvez le mettre en cache pour les futures réponses à ce thread de conversation si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="48761-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="48761-140">Meilleure pratique : messages de bienvenue dans teams</span><span class="sxs-lookup"><span data-stu-id="48761-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="48761-141">Lorsque votre bot est d’abord ajouté au groupe ou à l’équipe, il est généralement utile d’envoyer un message de bienvenue qui présente le bot à tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="48761-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="48761-142">Le message de bienvenue doit fournir une description de la fonctionnalité du robot et des avantages de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48761-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="48761-143">Idéalement, le message doit également inclure des commandes permettant à l’utilisateur d’interagir avec l’application.</span><span class="sxs-lookup"><span data-stu-id="48761-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="48761-144">Pour ce faire, vérifiez que votre robot répond au `conversationUpdate` message, avec le `teamsAddMembers` EventType dans l' `channelData` objet.</span><span class="sxs-lookup"><span data-stu-id="48761-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="48761-145">Assurez-vous `memberAdded` que l’ID est l’ID d’application du robot lui-même, car le même événement est envoyé lorsqu’un utilisateur est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="48761-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="48761-146">Pour plus d’informations, consultez la rubrique Ajout d’un [membre d’équipe ou](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) d’un robot.</span><span class="sxs-lookup"><span data-stu-id="48761-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="48761-147">Vous pouvez également envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté.</span><span class="sxs-lookup"><span data-stu-id="48761-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="48761-148">Pour ce faire, vous pouvez [extraire la liste de l’équipe](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) et envoyer un [message direct](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)à chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="48761-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="48761-149">Il est recommandé que votre bot *n’envoie pas* de message d’accueil dans les situations suivantes :</span><span class="sxs-lookup"><span data-stu-id="48761-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="48761-150">L’équipe est grande (évidemment subjective, mais par exemple, plus de 100 membres).</span><span class="sxs-lookup"><span data-stu-id="48761-150">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="48761-151">Votre robot peut être considéré comme « spammer » et la personne qui l’a ajouté peut recevoir des plaintes, sauf si vous communiquez clairement la proposition de valeur de votre robot à tous ceux qui voient le message de bienvenue.</span><span class="sxs-lookup"><span data-stu-id="48761-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="48761-152">Votre robot est d’abord mentionné dans un groupe ou un canal (et n’est pas d’abord ajouté à une équipe)</span><span class="sxs-lookup"><span data-stu-id="48761-152">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="48761-153">Un groupe ou un canal est renommé.</span><span class="sxs-lookup"><span data-stu-id="48761-153">A group or channel is renamed</span></span>
* <span data-ttu-id="48761-154">Un membre de l’équipe est ajouté à un groupe ou à un canal</span><span class="sxs-lookup"><span data-stu-id="48761-154">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="48761-155">@ Mentions</span><span class="sxs-lookup"><span data-stu-id="48761-155">@ Mentions</span></span>

<span data-ttu-id="48761-156">Étant donné que les robots d’un groupe ou d’un canal répondent uniquement lorsqu’ils sont mentionnés (« @_botname_») dans un message, chaque message reçu par un bot dans un canal de groupe contient son propre nom et vous devez vous assurer que le traitement de l’analyse des messages lui est propre.</span><span class="sxs-lookup"><span data-stu-id="48761-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="48761-157">De plus, les robots peuvent analyser les autres utilisateurs mentionnés et mentionner les utilisateurs dans leurs messages.</span><span class="sxs-lookup"><span data-stu-id="48761-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="48761-158">Récupération des mentions</span><span class="sxs-lookup"><span data-stu-id="48761-158">Retrieving mentions</span></span>

<span data-ttu-id="48761-159">Les mentions sont renvoyées `entities` dans l’objet dans la charge utile et contiennent l’ID unique de l’utilisateur et, dans la plupart des cas, le nom de l’utilisateur mentionné.</span><span class="sxs-lookup"><span data-stu-id="48761-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="48761-160">Vous pouvez récupérer toutes les mentions dans le message en appelant `GetMentions` la fonction dans le kit de développement logiciel (SDK) du générateur de `Mentioned` robots pour .net, qui renvoie un tableau d’objets.</span><span class="sxs-lookup"><span data-stu-id="48761-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="48761-161">Exemple de code .NET : Check for and Strip @bot mention</span><span class="sxs-lookup"><span data-stu-id="48761-161">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="48761-162">Vous pouvez également utiliser la fonction `GetTextWithoutMentions`d’extension de teams, qui supprime toutes les mentions, y compris le bot.</span><span class="sxs-lookup"><span data-stu-id="48761-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="48761-163">Exemple de code node. js : vérifier et supprimer @bot mention</span><span class="sxs-lookup"><span data-stu-id="48761-163">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="48761-164">Vous pouvez également utiliser la fonction `getTextWithoutMentions`d’extension de teams, qui supprime toutes les mentions, y compris le bot.</span><span class="sxs-lookup"><span data-stu-id="48761-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="48761-165">Création de mentions</span><span class="sxs-lookup"><span data-stu-id="48761-165">Constructing mentions</span></span>

<span data-ttu-id="48761-166">Votre robot peut mentionner d’autres utilisateurs dans les messages publiés dans des canaux.</span><span class="sxs-lookup"><span data-stu-id="48761-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="48761-167">Pour ce faire, votre message doit effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="48761-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="48761-168">Inclure `<at>@username</at>` dans le texte du message</span><span class="sxs-lookup"><span data-stu-id="48761-168">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="48761-169">Inclure l' `mention` objet à l’intérieur de la collection Entities</span><span class="sxs-lookup"><span data-stu-id="48761-169">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="48761-170">Exemple .NET</span><span class="sxs-lookup"><span data-stu-id="48761-170">.NET example</span></span>

<span data-ttu-id="48761-171">Cet exemple utilise le package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .</span><span class="sxs-lookup"><span data-stu-id="48761-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="48761-172">Exemple node. js</span><span class="sxs-lookup"><span data-stu-id="48761-172">Node.js example</span></span>

<span data-ttu-id="48761-173">Cet exemple utilise le package NPM [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) .</span><span class="sxs-lookup"><span data-stu-id="48761-173">This sample uses the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="48761-174">Exemple : message sortant avec l’utilisateur mentionné</span><span class="sxs-lookup"><span data-stu-id="48761-174">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="48761-175">Accès à l’étendue groupChat ou Channel</span><span class="sxs-lookup"><span data-stu-id="48761-175">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="48761-176">Votre robot peut faire plus que d’envoyer et de recevoir des messages dans les groupes et les équipes.</span><span class="sxs-lookup"><span data-stu-id="48761-176">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="48761-177">Par exemple, il peut également extraire la liste des membres, y compris leurs informations de profil, ainsi que la liste des canaux.</span><span class="sxs-lookup"><span data-stu-id="48761-177">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="48761-178">Pour en savoir plus, consultez [la rubrique obtenir le contexte de votre robot Microsoft teams](~/resources/bot-v3/bots-context.md) .</span><span class="sxs-lookup"><span data-stu-id="48761-178">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>
