---
title: Conversations de conversation de groupe et de canal avec les robots
description: Décrit le scénario de bout en bout d’une conversation avec un bot dans un canal dans Microsoft teams
keywords: scénarios teams-robots de conversation des canaux
ms.date: 06/25/2019
ms.openlocfilehash: d2d72bdba43de6ebb10c7504dd309459cb09d56c
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801094"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversations par chat de canal et de groupe avec un robot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft teams permet aux utilisateurs d’amener des robots à leurs conversations de conversation de groupe ou de canal. En ajoutant un bot à une équipe ou une conversation, tous les utilisateurs de la conversation peuvent tirer parti de la fonctionnalité de robot directement dans la conversation. Vous pouvez également accéder aux fonctionnalités propres à teams dans votre bot, telles que l’interrogation des informations d’équipe et des utilisateurs de @mentioning.

La conversation dans les canaux et les conversations de groupe diffèrent de la conversation personnelle en ce que l’utilisateur doit @mention le bot. Si un bot est utilisé dans plusieurs étendues (personnel, groupchat ou canal), vous devez détecter l’étendue d’origine des messages du bot et les traiter en conséquence.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Conception d’un robot idéal pour les canaux ou les groupes

Les robots ajoutés à une équipe deviennent un autre membre de l’équipe, qui peut être @mentioned dans le cadre de la conversation. En fait, les robots reçoivent uniquement les messages lorsqu’ils sont @mentioned, de sorte que les autres conversations sur le canal ne sont pas envoyées au bot.

> [!NOTE]
> Pour plus de commodité lors de la réponse à des messages de bot dans un canal, le nom du bot est automatiquement ajouté à la zone composer un message.

Un bot d’un groupe ou d’un canal doit fournir des informations pertinentes et appropriées pour tous les membres. Si votre robot peut certainement fournir des informations pertinentes pour l’expérience, gardez à l’esprit que les conversations sont visibles par tous les utilisateurs. Par conséquent, un bon robot d’un groupe ou d’un canal doit ajouter de la valeur à tous les utilisateurs et ne pas partager par inadvertance les informations de façon plus appropriée dans une conversation un-à-un.

Votre robot peut être entièrement pertinent dans toutes les étendues telles quelles et aucun travail supplémentaire significatif n’est nécessaire pour permettre à votre robot de travailler dessus. Dans Microsoft Teams, il n’y a aucune attente que votre bot fonctionne dans toutes les étendues, mais vous devez vous assurer que votre robot fournit la valeur de l’utilisateur dans n’importe quelle étendue que vous choisissez de prendre en charge. Pour plus d’informations sur les étendues, consultez la rubrique [applications dans Microsoft teams](~/concepts/build-and-test/app-studio-overview.md).

Le développement d’un bot qui fonctionne dans des groupes ou des canaux utilise la plupart des fonctionnalités des conversations personnelles. Les autres événements et données de la charge utile fournissent des informations sur le groupe teams et le canal. Ces différences, ainsi que les principales différences entre les fonctionnalités communes, sont décrites dans les sections suivantes.

### <a name="creating-messages"></a>Création de messages

Pour plus d’informations sur les robots de création de messages dans les canaux, consultez la rubrique [messagerie proactive pour les robots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)et [création d’une conversation de canal](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).

### <a name="receiving-messages"></a>Réception de messages

Pour un bot d’un groupe ou d’un canal, outre le [schéma de message normal](https://docs.botframework.com/core-concepts/reference/#activity), votre bot reçoit également les propriétés suivantes :

* `channelData`Voir [teams Channel Data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data). Dans une conversation de groupe, contient des informations spécifiques à cette conversation.
* `conversation.id`ID de la chaîne de réponse, composé de l’ID du canal plus l’ID du premier message de la chaîne de réponse.
* `conversation.isGroup`Est `true` destiné aux messages bot dans les canaux ou les conversations de groupe
* `conversation.conversationType`Soit `groupChat` ou`channel`
* `entities`Peut contenir une ou plusieurs mentions (voir [mentions](#-mentions))

### <a name="replying-to-messages"></a>Réponse aux messages

Pour répondre à un message existant, appelez [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) en .net ou [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) dans Node.js. Le kit de développement logiciel (SDK) du générateur de robots gère tous les détails.

Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) point de terminaison.

Dans un canal, la réponse à un message apparaît sous la forme d’une réponse à la chaîne de réponse initiale. Le `conversation.id` contient le canal et l’ID de message de niveau supérieur. Bien que l’infrastructure de bot prenne en charge les détails, vous pouvez le mettre en cache `conversation.id` pour les futures réponses à ce thread de conversation si nécessaire.

### <a name="best-practice-welcome-messages-in-teams"></a>Meilleure pratique : messages de bienvenue dans teams

Lorsque votre bot est d’abord ajouté au groupe ou à l’équipe, il est généralement utile d’envoyer un message de bienvenue qui présente le bot à tous les utilisateurs. Le message de bienvenue doit fournir une description de la fonctionnalité du robot et des avantages de l’utilisateur. Idéalement, le message doit également inclure des commandes permettant à l’utilisateur d’interagir avec l’application. Pour ce faire, vérifiez que votre robot répond au `conversationUpdate` message, avec le `teamsAddMembers` eventType dans l' `channelData` objet. Assurez-vous que l' `memberAdded` ID est l’ID d’application du robot lui-même, car le même événement est envoyé lorsqu’un utilisateur est ajouté à une équipe. Pour plus d’informations, consultez la rubrique Ajout d’un [membre d’équipe ou](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) d’un robot.

Vous pouvez également envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté. Pour ce faire, vous pouvez [extraire la liste de l’équipe](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) et envoyer un [message direct](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)à chaque utilisateur.

Il est recommandé que votre bot *n’envoie pas* de message d’accueil dans les situations suivantes :

* L’équipe est grande (évidemment subjective, mais par exemple, plus de 100 membres). Votre robot peut être considéré comme « spammer » et la personne qui l’a ajouté peut recevoir des plaintes, sauf si vous communiquez clairement la proposition de valeur de votre robot à tous ceux qui voient le message de bienvenue.
* Votre robot est d’abord mentionné dans un groupe ou un canal (et n’est pas d’abord ajouté à une équipe)
* Un groupe ou un canal est renommé.
* Un membre de l’équipe est ajouté à un groupe ou à un canal

## <a name="-mentions"></a>@ Mentions

Étant donné que les robots d’un groupe ou d’un canal répondent uniquement lorsqu’ils sont mentionnés (« @_botname_») dans un message, chaque message reçu par un bot dans un canal de groupe contient son propre nom et vous devez vous assurer que le traitement de l’analyse des messages lui est propre. De plus, les robots peuvent analyser les autres utilisateurs mentionnés et mentionner les utilisateurs dans leurs messages.

### <a name="retrieving-mentions"></a>Récupération des mentions

Les mentions sont renvoyées dans l' `entities` objet dans la charge utile et contiennent l’ID unique de l’utilisateur et, dans la plupart des cas, le nom de l’utilisateur mentionné. Vous pouvez récupérer toutes les mentions dans le message en appelant la `GetMentions` fonction dans le kit de développement logiciel (SDK) du générateur de robots pour .net, qui renvoie un tableau d' `Mentioned` objets.

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Exemple de code .NET : Check for and Strip @bot mention

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
> Vous pouvez également utiliser la fonction d’extension de teams `GetTextWithoutMentions` , qui supprime toutes les mentions, y compris le bot.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Exemple de code Node.js : Check for and Strip @bot mention

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

Vous pouvez également utiliser la fonction d’extension de teams `getTextWithoutMentions` , qui supprime toutes les mentions, y compris le bot.

### <a name="constructing-mentions"></a>Création de mentions

Votre robot peut mentionner d’autres utilisateurs dans les messages publiés dans des canaux. Pour ce faire, votre message doit effectuer les opérations suivantes :

* Inclure `<at>@username</at>` dans le texte du message
* Inclure l' `mention` objet à l’intérieur de la collection Entities

#### <a name="net-example"></a>Exemple .NET

Cet exemple utilise le package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Exemple de Node.js

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>Exemple : message sortant avec l’utilisateur mentionné

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

## <a name="accessing-groupchat-or-channel-scope"></a>Accès à l’étendue groupChat ou Channel

Votre robot peut faire plus que d’envoyer et de recevoir des messages dans les groupes et les équipes. Par exemple, il peut également extraire la liste des membres, y compris leurs informations de profil, ainsi que la liste des canaux. Pour en savoir plus, consultez [la rubrique obtenir le contexte de votre robot Microsoft teams](~/resources/bot-v3/bots-context.md) .

*Voir aussi* [exemples de robots d’infrastructure](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).
