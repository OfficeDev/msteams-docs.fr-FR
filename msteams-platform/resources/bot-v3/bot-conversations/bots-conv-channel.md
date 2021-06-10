---
title: Conversations de conversation de canal et de groupe avec des bots
description: Décrit le scénario de bout en bout d’une conversation avec un bot dans un canal Microsoft Teams
keywords: teams scenarios channels conversation bot
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e254302271cf101638c897e1a1952d302705d6a4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566795"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>Conversations par chat de canal et de groupe avec un robot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams permet aux utilisateurs d’amener des bots dans leurs conversations de canal ou de groupe. En ajoutant un bot à une équipe ou à une conversation, tous les utilisateurs de la conversation peuvent tirer parti des fonctionnalités du bot directement dans la conversation. Vous pouvez également accéder Teams fonctionnalités spécifiques au sein de votre bot, telles que l’interrogation d’informations d’équipe et @mentioning utilisateurs.

La conversation dans les canaux et les conversations de groupe diffère de la conversation personnelle, dans la fait que l’utilisateur doit @mention le bot. Si un bot est utilisé dans plusieurs étendues telles que personnel, groupchat ou canal, vous devez détecter l’étendue d’où les messages du bot sont issus et les traiter en conséquence.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Conception d’un bot idéal pour les canaux ou les groupes

Les bots ajoutés à une équipe deviennent un autre membre de l’équipe et peuvent être @mentioned dans le cadre de la conversation. En fait, les bots reçoivent des messages uniquement lorsqu’ils @mentioned, de sorte que les autres conversations sur le canal ne sont pas envoyées au bot.

Un bot dans un groupe ou un canal doit fournir des informations pertinentes et appropriées pour tous les membres. Bien que votre bot puisse certainement fournir des informations pertinentes pour l’expérience, gardez à l’esprit que les conversations avec elle sont visibles par tout le monde. Par conséquent, un bot efficace dans un groupe ou un canal doit ajouter de la valeur à tous les utilisateurs et ne pas partager par inadvertance des informations plus appropriées à une conversation un-à-un.

Votre bot, comme il est, peut être entièrement pertinent dans toutes les étendues sans nécessiter de travail supplémentaire. Dans Microsoft Teams il n’est pas attendu que votre bot fonctionne dans toutes les étendues, mais vous devez vous assurer que votre bot fournit une valeur utilisateur dans n’importe quelle étendue que vous choisissez de prendre en charge. Pour plus d’informations sur les étendues, voir [Applications dans Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).

Le développement d’un bot qui fonctionne dans des groupes ou des canaux utilise la plupart des mêmes fonctionnalités que les conversations personnelles. Des événements et des données supplémentaires dans la charge utile fournissent des Teams de groupe et de canal. Ces différences, ainsi que les principales différences de fonctionnalités courantes, sont décrites dans les sections suivantes.

### <a name="creating-messages"></a>Création de messages

Pour plus d’informations sur les bots qui créent des messages dans les canaux, voir Messagerie proactive pour les [bots,](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)et plus spécifiquement Création [d’une conversation de canal.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)

### <a name="receiving-messages"></a>Réception de messages

Pour un bot dans un groupe ou un canal, en plus du schéma de [message](https://docs.botframework.com/core-concepts/reference/#activity)normal, votre bot reçoit également les propriétés suivantes :

* `channelData`Voir [Teams données du canal de distribution.](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data) Dans une conversation de groupe, contient des informations spécifiques à cette conversation.
* `conversation.id` ID de chaîne de réponse, constitué de l’ID de canal et de l’ID du premier message de la chaîne de réponse.
* `conversation.isGroup``true`S’agit des messages de bot dans les canaux ou les conversations de groupe.
* `conversation.conversationType` Soit `groupChat` ou `channel` .
* `entities` Peut contenir une ou plusieurs mentions. Pour plus d’informations, voir [Mentions.](#-mentions)

### <a name="replying-to-messages"></a>Réponse aux messages

Pour répondre à un message existant, [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) appelez .NET ou [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) dans Node.js. Le SDK Bot Builder gère tous les détails.

Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) point de terminaison.

Dans un canal, la réponse à un message s’affiche comme une réponse à la chaîne de réponse à l’origine. Contient `conversation.id` le canal et l’ID de message de niveau supérieur. Bien que Bot Framework s’occupe des détails, vous pouvez le mettre en cache pour les réponses ultérieures à ce `conversation.id` thread de conversation si nécessaire.

### <a name="best-practice-welcome-messages-in-teams"></a>Meilleure pratique : messages de bienvenue dans Teams

Lorsque votre bot est ajouté pour la première fois au groupe ou à l’équipe, il est généralement utile d’envoyer un message de bienvenue présentant le bot à tous les utilisateurs. Le message de bienvenue doit fournir une description des fonctionnalités et des avantages du bot pour les utilisateurs. Dans l’idéal, le message doit également inclure des commandes pour permettre à l’utilisateur d’interagir avec l’application. Pour ce faire, assurez-vous que votre bot répond au message, avec `conversationUpdate` `teamsAddMembers` l’eventType dans `channelData` l’objet. Assurez-vous que l’ID est lui-même l’ID d’application du bot, car le même événement est envoyé lorsqu’un utilisateur est ajouté `memberAdded` à une équipe. Pour plus [d’informations, voir l’ajout](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) d’un membre d’équipe ou d’un bot.

Vous pouvez également envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté. Pour ce faire, vous pouvez récupérer [la liste de](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) l’équipe et envoyer un message direct à chaque [utilisateur.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

Il est recommandé que votre bot *n’envoie* pas de message de bienvenue dans les situations suivantes :

* L’équipe est grande (bien évidemment subjectif, par exemple, plus de 100 membres). Votre bot peut être considéré comme « spammy » et la personne qui l’a ajouté peut obtenir des réclamations, sauf si vous communiquez clairement la proposition de valeur de votre bot à toutes les personnes qui voient le message de bienvenue.
* Votre bot est d’abord mentionné dans un groupe ou un canal, plutôt que d’être ajouté pour la première fois à une équipe.
* Un groupe ou un canal est renommé.
* Un membre d’équipe est ajouté à un groupe ou un canal.

## <a name="-mentions"></a>@ Mentions

Étant donné que les bots d’un groupe ou d’un canal répondent uniquement lorsqu’ils sont mentionnés (« @_botname_») dans un message, chaque message reçu par un bot dans un canal de groupe contient son propre nom, et vous devez vous assurer que votre message est traité par l’ensemble des messages. En outre, les bots peuvent passer en détail d’autres utilisateurs mentionnés et mentionner des utilisateurs dans le cadre de leurs messages.

### <a name="retrieving-mentions"></a>Récupération des mentions

Les mentions sont renvoyées dans l’objet dans la charge utile et contiennent l’ID unique de l’utilisateur et, dans la plupart des cas, le nom de `entities` l’utilisateur mentionné. Vous pouvez récupérer toutes les mentions dans le message en appelant la fonction dans le SDK Bot Builder pour .NET, qui renvoie un tableau `GetMentions` `Mentioned` d’objets.

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>Exemple de code .NET : vérifier et @bot mention

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
> Vous pouvez également utiliser la fonction d Teams d’extension, qui permet d’enlever toutes les `GetTextWithoutMentions` mentions, y compris le bot.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js exemple de code : Vérifier et @bot mention

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

Vous pouvez également utiliser la fonction d Teams d’extension, qui permet d’enlever toutes les `getTextWithoutMentions` mentions, y compris le bot.

### <a name="constructing-mentions"></a>Construction de mentions

Votre bot peut mentionner d’autres utilisateurs dans les messages publiés dans les canaux. Pour ce faire, votre message doit :

* Inclure `<at>@username</at>` dans le texte du message.
* Inclure `mention` l’objet à l’intérieur de la collection d’entités.

#### <a name="net-example"></a>Exemple .NET

Cet exemple utilise le package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Node.js exemple

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>Exemple : message sortant avec l’utilisateur mentionné

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

## <a name="accessing-groupchat-or-channel-scope"></a>Accès à l’étendue groupChat ou canal

Votre bot peut faire plus que d’envoyer et de recevoir des messages dans des groupes et des équipes. Par exemple, il peut également récupérer la liste des membres, y compris leurs informations de profil, ainsi que la liste des canaux. Pour plus d’informations, [voir Obtenir le contexte de votre bot Microsoft Teams.](~/resources/bot-v3/bots-context.md)

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
