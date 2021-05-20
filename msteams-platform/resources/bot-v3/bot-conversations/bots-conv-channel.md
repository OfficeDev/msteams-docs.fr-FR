---
title: Conversations de chat de canal et de groupe avec des bots
description: Décrit le scénario de bout en bout d’avoir une conversation avec un bot dans un canal dans Microsoft Teams
keywords: scénarios équipes canaux conversation bot
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

Microsoft Teams permet aux utilisateurs d’apporter des bots dans leurs conversations de chat de canal ou de groupe. En ajoutant un bot à une équipe ou à un chat, tous les utilisateurs de la conversation peuvent profiter de la fonctionnalité du bot directement dans la conversation. Vous pouvez également accéder à Teams spécifiques à votre bot, comme interroger les informations de l’équipe et @mentioning utilisateurs.

Chat dans les canaux et les chats de groupe diffèrent de chat personnel en ce que l’utilisateur a besoin @mention le bot. Si un bot est utilisé dans plusieurs étendues telles que personnel, groupchat, ou canal, vous devez détecter quelle portée les messages bot provenaient, et les traiter en conséquence.

## <a name="designing-a-great-bot-for-channels-or-groups"></a>Concevoir un grand bot pour les canaux ou les groupes

Les bots ajoutés à une équipe deviennent un autre membre de l’équipe et peuvent @mentioned dans le cadre de la conversation. En fait, les bots ne reçoivent des messages que lorsqu’ils @mentioned, de sorte que d’autres conversations sur le canal ne sont pas envoyées au bot.

Un bot dans un groupe ou un canal doit fournir des informations pertinentes et appropriées pour tous les membres. Bien que votre bot peut certainement fournir toutes les informations pertinentes à l’expérience, gardez à l’esprit les conversations avec elle sont visibles pour tout le monde. Par conséquent, un grand bot dans un groupe ou un canal devrait ajouter de la valeur à tous les utilisateurs, et certainement pas par inadvertance partager des informations plus appropriées à une conversation en tête-à-tête.

Votre bot, tel qu’il est, peut être entièrement pertinent dans toutes les étendues sans nécessiter de travail supplémentaire. En Microsoft Teams il n’y a aucune attente que votre fonction bot dans toutes les étendues, mais vous devez vous assurer que votre bot fournit la valeur utilisateur dans n’importe quelle portée (s) que vous choisissez de prendre en charge. Pour plus d’informations sur les étendues, [voir Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).

Le développement d’un bot qui fonctionne en groupes ou en canaux utilise une grande partie de la même fonctionnalité que les conversations personnelles. D’autres événements et données dans la charge utile fournissent Teams informations sur le groupe et le canal. Ces différences, ainsi que les principales différences dans les fonctionnalités communes sont décrites dans les sections suivantes.

### <a name="creating-messages"></a>Création de messages

Pour plus d’informations sur les bots créant des messages dans les canaux [voir messagerie proactive pour les bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), et en particulier la création [d’une conversation canal](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).

### <a name="receiving-messages"></a>Réception de messages

Pour un bot dans un groupe ou un canal, en plus du [schéma de message régulier,](https://docs.botframework.com/core-concepts/reference/#activity)votre bot reçoit également les propriétés suivantes:

* `channelData`Voir [Teams données du canal](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data). Dans un chat de groupe, contient des informations spécifiques à ce chat.
* `conversation.id` L’ID de la chaîne de réponse, composé de l’ID du canal plus l’ID du premier message dans la chaîne de réponse.
* `conversation.isGroup` Est pour `true` les messages bot dans les canaux ou les chats de groupe.
* `conversation.conversationType` Soit `groupChat` ou `channel` .
* `entities` Peut contenir une ou plusieurs mentions. Pour plus d’informations, voir [Mentions](#-mentions).

### <a name="replying-to-messages"></a>Répondre aux messages

Pour répondre à un message existant, [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) appelez .NET ou [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) en Node.js. Le Bot Builder SDK gère tous les détails.

Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le point [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) de terminaison.

Dans un canal, répondre à un message s’affiche comme une réponse à la chaîne de réponse initiatrice. Le `conversation.id` contient le canal et l’ID de message de niveau supérieur. Bien que le Cadre Bot s’occupe des détails, vous pouvez mettre en cache `conversation.id` que pour les réponses futures à ce fil de conversation au besoin.

### <a name="best-practice-welcome-messages-in-teams"></a>Meilleures pratiques : Messages de bienvenue dans Teams

Lorsque votre bot est ajouté pour la première fois au groupe ou à l’équipe, il est généralement utile d’envoyer un message de bienvenue introduisant le bot à tous les utilisateurs. Le message de bienvenue doit fournir une description des fonctionnalités du bot et des avantages pour l’utilisateur. Idéalement, le message doit également inclure des commandes pour que l’utilisateur interagit avec l’application. Pour ce faire, assurez-vous que votre bot répond au `conversationUpdate` message, avec `teamsAddMembers` l’eventType dans `channelData` l’objet. Assurez-vous que `memberAdded` l’ID est l’iD app du bot lui-même, car le même événement est envoyé lorsqu’un utilisateur est ajouté à une équipe. Voir membre [de l’équipe ou ajout de bot pour](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) plus de détails.

Vous pouvez également envoyer un message personnel à chaque membre de l’équipe lorsque le bot est ajouté. Pour ce faire, vous pouvez aller [chercher la liste de l’équipe](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) et envoyer un message direct à chaque [utilisateur.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

Nous recommandons à votre bot de *ne pas* envoyer un message de bienvenue dans les situations suivantes :

* L’équipe est grande (évidemment subjective, par exemple, plus de 100 membres). Votre bot peut être considéré comme « spamme » et la personne qui l’a ajouté peut obtenir des plaintes, sauf si vous communiquez clairement la proposition de valeur de votre bot à tous ceux qui voient le message de bienvenue.
* Votre bot est d’abord mentionné dans un groupe ou un canal, plutôt que d’être ajouté pour la première fois à une équipe.
* Un groupe ou un canal est renommé.
* Un membre de l’équipe est ajouté à un groupe ou à un canal.

## <a name="-mentions"></a>@ Mentions

Étant donné que les bots d’un groupe ou d’un canal ne répondent que lorsqu’ils sont mentionnés (« @_botname »)_ dans un message, chaque message reçu par un bot dans un canal de groupe contient son propre nom, et vous devez vous assurer que votre message parsing gère cela. En outre, les bots peuvent parse d’autres utilisateurs mentionnés et mentionner les utilisateurs dans le cadre de leurs messages.

### <a name="retrieving-mentions"></a>Récupération des mentions

Les mentions sont retournées dans `entities` l’objet en charge utile et contiennent à la fois l’identifiant unique de l’utilisateur et, dans la plupart des cas, le nom de l’utilisateur mentionné. Vous pouvez récupérer toutes les mentions dans le message en appelant la `GetMentions` fonction dans le Bot Builder SDK pour .NET, qui renvoie un tableau d’objets. `Mentioned`

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET exemple de code: Vérifiez et dépouillez @bot mention

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
> Vous pouvez également utiliser la fonction Teams’extension `GetTextWithoutMentions` de la bouteille, qui enlève toutes les mentions, y compris le bot.

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js code d’exemple : Vérifiez et dépouillez @bot mention

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

Vous pouvez également utiliser la fonction Teams’extension `getTextWithoutMentions` de la bouteille, qui enlève toutes les mentions, y compris le bot.

### <a name="constructing-mentions"></a>Construction de mentions

Votre bot peut mentionner d’autres utilisateurs dans les messages postés dans les canaux. Pour ce faire, votre message doit faire ce qui suit :

* Inclure `<at>@username</at>` dans le texte du message.
* Incluez `mention` l’objet à l’intérieur de la collection des entités.

#### <a name="net-example"></a>Exemple .NET

Cet exemple utilise le [paquet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>Exemple : Message sortant avec l’utilisateur mentionné

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

## <a name="accessing-groupchat-or-channel-scope"></a>Accès à groupChat ou portée de canal

Votre bot peut faire plus que d’envoyer et de recevoir des messages en groupes et en équipes. Par exemple, il peut également aller chercher la liste des membres, y compris leurs informations de profil, ainsi que la liste des canaux. Pour plus d’informations, [voir Obtenez le contexte de votre Microsoft Teams bot](~/resources/bot-v3/bots-context.md).

## <a name="see-also"></a>Voir aussi

[Échantillons de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
