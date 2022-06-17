---
title: Envoyer et recevoir des messages avec un bot
description: Dans ce module, apprenez à avoir une conversation avec un bot Microsoft Teams, des messages proactifs, des notions de base de conversation, du contenu et de la mise en forme des messages
ms.topic: overview
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: fdf408a9e9d49c9c5c862a6b4dda3c7db7de93e8
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143388"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Avoir une conversation avec un bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs. Il existe trois types de conversations (ou portées) dans Teams :

* `teams` également appelés conversations de canal, visibles par tous les membres du canal.
* `personal` conversations entre les bots et un seul utilisateur.
* `groupChat` Conversation entre un bot et au moins deux utilisateurs.

Le comportement d’un bot peut varier légèrement selon le type de conversation à laquelle il participe:

* [Bots dans les conversations de canal et de groupe](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) demander à l’utilisateur de @mention le bot pour l’appeler dans un canal.
* Les [bots dans les conversations mono-utilisateur](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) ne nécessitent pas de @mention – l’utilisateur peut simplement taper.

Pour que le bot fonctionne dans une étendue particulière, il doit être répertorié comme prenant en charge cette étendue dans le manifeste. Les étendues sont définies et discutées plus en détail dans la [référence du manifeste](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Messages proactifs

Les bots peuvent participer à une conversation ou en lancer une. La plupart des communications sont en réponse à un autre message. Si un bot initie une conversation, cela s’appelle un *message proactif*. Les exemples incluent :

* Les messages de bienvenue
* Notifications d’événement
* Interrogation des messages

## <a name="conversation-basics"></a>Concepts de base d’une conversation

Chaque message est un objet `Activity` de type `messageType: message`. Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot. Votre bot examine le message pour déterminer son type et répond en conséquence.

Les bots prennent également en charge les messages de style événement. Pour plus d’informations, consultez [Gérer les événements de bot dans Microsoft Teams](~/resources/bot-v3/bots-notifications.md). La reconnaissance vocale n’est actuellement pas prise en charge.

Les messages sont généralement les mêmes dans toutes les étendues, mais il existe des différences dans la façon dont le bot est accessible dans l’interface utilisateur et des différences dans les coulisses, que vous devez connaître.

La conversation de base est gérée via le connecteur Bot Framework, une API REST unique permettant à votre bot de communiquer avec Teams et d’autres canaux. Le Kit de développement logiciel (SDK) Bot Builder fournit un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux et l’état des conversations, ainsi que des moyens simples d’incorporer des services cognitifs tels que le traitement en langage naturel (NLP).

## <a name="message-content"></a>Contenu du message

Votre bot peut envoyer du texte enrichi, des images et des cartes. Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot. Vous pouvez spécifier le type de contenu que votre bot peut gérer dans la page des paramètres Microsoft Teams de votre bot.

| Format | De l’utilisateur au bot  | Du bot à l’utilisateur |  Notes |
| --- | :---: | :---: | --- |
| Texte enrichi  | ✔ | ✔ |  |
| Images | ✔ | ✔ | Maximum 1024 × 1024 Mo et 1 Mo au format PNG, JPEG ou GIF ; Les GIF animés ne sont pas pris en charge. |
| Cartes | ✖ | ✔ | Consultez la [référence de carte Teams](~/task-modules-and-cards/cards/cards-reference.md) pour les cartes prises en charge. |
| Emojis | ✖ | ✔ | Teams prend actuellement en charge les emojis via UTF-16 comme U+1F600 pour les visages souriants. |
|

Pour plus d’informations sur les types d’interaction de bot pris en charge par Bot Framework, sur lesquels les bots des équipes sont basés, consultez la documentation bot framework sur le [flux de conversation](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) et les concepts connexes dans la documentation [du Kit de développement logiciel (SDK) Bot Builder pour .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) et [du Kit de développement logiciel Bot Builder pour Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).

## <a name="message-formatting"></a>Mise en forme de messages

Vous pouvez définir la propriété [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) facultative d’un `message` pour contrôler le rendu du contenu texte de votre message. Consultez [la mise en forme des messages](~/resources/bot-v3/bots-message-format.md) pour obtenir une description détaillée de la mise en forme prise en charge dans les messages de bot.
Vous pouvez définir la propriété [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) facultative pour contrôler le rendu du contenu texte de votre message.

Pour plus d’informations sur la façon dont Teams prend en charge la mise en forme de texte dans les équipes, consultez [Mise en forme de texte dans les messages de bot](~/resources/bot-v3/bots-text-formats.md).

Pour plus d’informations sur la mise en forme des cartes dans les messages, consultez [Mise en forme des cartes](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Messages d’image

Les images sont envoyées en ajoutant des pièces jointes à un message. Vous trouverez plus d’informations sur les pièces jointes dans la documentation [Bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).

Les images peuvent avoir au maximum 1 024×1 024 Mo et 1 Mo au format PNG, JPEG ou GIF ; GIF animé n’est pas pris en charge.

Nous vous recommandons de spécifier la hauteur et la largeur de chaque image à l’aide de XML. Si vous utilisez Markdown, la taille par défaut de l’image est 256x256. Par exemple :

* Utiliser `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Ne pas utiliser `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Réception de messages

Selon les étendues déclarées, votre bot peut recevoir des messages dans les contextes suivants :

* **chat personnel** Les utilisateurs peuvent interagir dans une conversation privée avec un bot en sélectionnant le bot ajouté dans l’historique du chat, ou en tapant son nom ou son ID d’application dans le champ À : sur un nouveau chat.
* **Canaux** Un bot peut être mentionné (« @*botname*») dans un canal s’il a été ajouté à l’équipe. Notez que les réponses supplémentaires à un bot dans un canal nécessitent la mention du bot. Il ne répondra pas aux réponses où il n’est pas mentionné.

Pour les messages entrants, votre bot reçoit un objet [Activity](../../../bots/how-to/conversations/conversation-messages.md) de type `messageType: message`. Bien que l’`Activity`objet puisse contenir d’autres types d’informations, comme les [mises à jour de canal](~/resources/bot-v3/bots-notifications.md#channel-updates) envoyées à votre bot, le type `message` représente la communication entre le bot et l’utilisateur.

Votre bot reçoit une charge utile qui contient le message de l’utilisateur `Text` et d’autres informations sur l’utilisateur, la source du message et les informations Teams. À noter :

* `timestamp`Date et heure à l’heure UTC (temps universel coordonné) au moment où l’utilisateur a cliqué sur l’URL.
* `localTimestamp` Date et heure du message dans le fuseau horaire de l’expéditeur.
* `channelId` Toujours "msteams". Cela fait référence à un canal de structure de bot, pas à un canal d’équipes.
* `from.id` un ID unique et chiffré pour cet utilisateur pour votre bot ; convient en tant que clé si votre application doit stocker des données utilisateur. Il est unique pour votre bot et ne peut pas être utilisé directement en dehors de votre instance de bot de manière significative pour identifier cet utilisateur.
* `channelData.tenant.id` L’ID de locataire de l’utilisateur.

> [!NOTE]
> `from.id` est unique pour votre bot et ne peut pas être utilisé directement en dehors de votre instance de bot de manière significative pour identifier cet utilisateur.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Combinaison de canaux et d’interactions privées avec votre bot

Lorsque vous interagissez dans un canal, votre bot doit être intelligent pour mettre certaines conversations hors connexion avec un utilisateur. Par exemple, supposons qu’un utilisateur tente de coordonner une tâche complexe, telle que la planification avec un ensemble de membres de l’équipe. Plutôt que d’avoir l’ensemble de la séquence d’interactions visible par le canal, envisagez d’envoyer un message de conversation personnel à l’utilisateur. Votre bot doit être en mesure de migrer facilement l’utilisateur entre les conversations personnelles et les conversations de canal sans perdre l’état.

> [!NOTE]
>N’oubliez pas de mettre à jour le canal une fois l’interaction terminée pour avertir les autres membres de l’équipe.

## <a name="full-inbound-schema-example"></a>Exemple de schéma entrant complet

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

> [!NOTE]
> Le champ de texte des messages entrants contient parfois des mentions. Veillez à les vérifier et à les supprimer correctement. Pour plus d’informations, consultez [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>Données du canal Teams

L’objet `channelData` contient des informations spécifiques à Teams et constitue la source définitive des ID d’équipe et de canal. Vous devez mettre en cache et utiliser ces ID comme clés pour le stockage local.

Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :

* `eventType` Type d’événement Teams ; passé uniquement en cas d’[événements de modification de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `tenant.id`Microsoft Azure Active Directory (Azure AD) ID de locataire ; transmis dans tous les contextes.
* `team` passé uniquement dans les contextes de canal, et non dans la conversation personnelle.
  * `id` GUID pour le canal.
  * `name` Nom de l’équipe ; passé uniquement en cas [d’événements de changement de nom d’équipe](~/resources/bot-v3/bots-notifications.md#team-name-updates).
* `channel` passé uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux des équipes où le bot a été ajouté.
  * `id` GUID pour le canal.
  * `name` Nom du canal ; transmis uniquement en cas [d’événements de modification de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `channelData.teamsTeamId` Obsolète. Cette propriété n’est incluse qu’à des fins de rétrocompatibilité.
* `channelData.teamsChannelId` Obsolète. Cette propriété n’est incluse qu’à des fins de rétrocompatibilité.

### <a name="example-channeldata-object-channelcreated-event"></a>Exemple d’objet channelData (événement channelCreated)

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

### <a name="net-example"></a>Exemple .NET

Le package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet fournit un objet spécialisé `TeamsChannelData` qui expose les propriétés pour accéder aux informations spécifiques à Teams.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Envoi de réponses à des messages

Pour répondre à un message existant, appelez [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) .NET ou [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) dans Node.js. Le Kit de développement logiciel (SDK) Bot Builder gère tous les détails.

Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le point de terminaison [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true).

Le contenu du message lui-même peut contenir du texte simple ou certaines des Bot Framework fournies [cartes et actions de carte](~/task-modules-and-cards/cards/cards-actions.md).

Notez que dans votre schéma sortant, vous devez toujours utiliser le même `serviceUrl` que celui que vous avez reçu. N’oubliez pas que la valeur de `serviceUrl` a tendance à être stable, mais qu’elle peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée de `serviceUrl`.

## <a name="updating-messages"></a>Mise à jour des messages

Au lieu que vos messages soient des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages en ligne après les avoir envoyés. Vous pouvez utiliser des mises à jour de messages dynamiques pour des scénarios tels que les mises à jour de sondage, la modification des actions disponibles après une pression sur un bouton ou tout autre changement d’état asynchrone.

Le nouveau message ne doit pas nécessairement correspondre à l’original dans le type. Par exemple, si le message d’origine contenait une pièce jointe, le nouveau message peut être un message texte.

> [!NOTE]
> Vous pouvez mettre à jour uniquement le contenu envoyé dans les messages à pièce jointe unique et les dispositions de carrousel. La publication de mises à jour de messages comportant plusieurs pièces jointes dans la disposition de liste n’est pas prise en charge.

### <a name="rest-api"></a>API REST

Pour émettre une mise à jour de message, exécutez une requête PUT sur le point de terminaison à l’aide `/v3/conversations/<conversationId>/activities/<activityId>/` d’un ID d’activité donné. Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité retourné par l’appel POST d’origine.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Exemple .NET

Vous pouvez utiliser la méthode `UpdateActivityAsync` dans le SDK Bot Builder pour mettre à jour un message existant.

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a>Exemple Node.js

Vous pouvez utiliser la méthode `session.connector.update` dans le SDK Bot Builder pour mettre à jour un message existant.

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a>Démarrage d’une conversation (messagerie proactive)

Vous pouvez créer une conversation personnelle avec un utilisateur ou démarrer une nouvelle chaîne de réponse dans un canal pour votre bot d’équipe. Cela vous permet d’envoyer un message à votre ou vos utilisateurs sans qu’ils aient d’abord pris contact avec votre bot. Si vous souhaitez en savoir plus, consultez les articles suivants :

Consultez [messagerie proactive pour les bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) pour plus d’informations générales sur les conversations démarrées par les bots.

## <a name="deleting-messages"></a>Suppression de messages

Les messages peuvent être supprimés à l’aide de la méthode connecteurs [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html) dans le [Kit de développement logiciel (SDK) BotBuilder](/bot-framework/bot-builder-overview-getstarted).

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
