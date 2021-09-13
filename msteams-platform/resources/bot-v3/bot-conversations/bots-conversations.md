---
title: Envoyer et recevoir des messages avec un bot
description: Décrit comment envoyer et recevoir des messages avec des bots Microsoft Teams
ms.topic: overview
ms.localizationpriority: medium
keywords: messages de bots teams
ms.date: 05/20/2019
ms.openlocfilehash: c82f96c42992f49f61d19c2bf5c6a19283e8ee95
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155877"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Avoir une conversation avec un bot Microsoft Teams’équipe

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs. Il existe trois types de conversations (ou portées) dans Teams :

* `teams` Également appelées conversations de canal, visibles par tous les membres du canal.
* `personal` Conversations entre les bots et un seul utilisateur.
* `groupChat` Discutez entre un bot et au moins deux utilisateurs.

Un bot se comporte légèrement différemment selon le type de conversation dans qui il est impliqué :

* [Les bots dans les conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) de canal et de groupe nécessitent que l’utilisateur @mention le bot pour l’appeler dans un canal.
* [Les bots dans les conversations d’un](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) seul utilisateur ne nécessitent pas de @mention - l’utilisateur peut simplement taper.

Pour que le bot fonctionne dans une étendue particulière, il doit être répertorié en tant que prise en charge de cette étendue dans le manifeste. Les étendues sont définies et abordées plus en détail dans la [Référence du manifeste.](~/resources/schema/manifest-schema.md)

## <a name="proactive-messages"></a>Messages proactifs

Les bots peuvent participer à une conversation ou en initier une. La plupart des communications sont en réponse à un autre message. Si un bot initie une conversation, il s’agit *d’un message proactif.* Les exemples incluent :

* Les messages de bienvenue
* Notifications d’événement
* Interrogation des messages

## <a name="conversation-basics"></a>Concepts de base d’une conversation

Chaque message est un objet `Activity` de type `messageType: message`. Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot. Votre bot examine le message pour déterminer son type et répond en conséquence.

Les bots supportent également les messages de type événement. Pour plus d’informations, voir [Gérer les événements de bot dans Microsoft Teams](~/resources/bot-v3/bots-notifications.md). La reconnaissance vocale n’est actuellement pas prise en charge.

Les messages sont pour la plupart identiques dans toutes les étendues, mais il existe des différences dans l’accès au bot dans l’interface utilisateur et des différences en arrière-plan que vous devez connaître.

La conversation de base est gérée par le biais du connecteur Bot Framework, une API REST unique permettant à votre bot de communiquer avec Teams et d’autres canaux. Le SDK Bot Builder fournit un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux et l’état des conversations, ainsi que des moyens simples d’incorporer des services cognitives tels que le traitement du langage naturel (NLP).

## <a name="message-content"></a>Contenu du message

Votre bot peut envoyer du texte enrichi, des images et des cartes. Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot. Vous pouvez spécifier le type de contenu que votre bot peut gérer dans la page Microsoft Teams paramètres de votre bot.

| Format | De l’utilisateur au bot  | Du bot à l’utilisateur |  Remarques |
| --- | :---: | :---: | --- |
| Texte enrichi  | ✔ | ✔ |  |
| Images | ✔ | ✔ | Maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge. |
| Cartes | ✖ | ✔ | Voir la référence [Teams carte de visite](~/task-modules-and-cards/cards/cards-reference.md) pour les cartes pris en charge. |
| Emojis | ✖ | ✔ | Teams prend actuellement en charge les emojis via UTF-16, par exemple, U+1F600 pour le visage de panoramique. |
|

Pour plus d’informations sur les types d’interaction de bot pris en charge par Bot Framework, sur lesquels les bots dans les équipes sont basés, voir la documentation Bot Framework sur le flux de [conversation](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) et les concepts associés dans la documentation du [SDK Bot Builder](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) pour .NET et du [SDK Bot Builder ](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)pour Node.js.

## <a name="message-formatting"></a>Mise en forme de messages

Vous pouvez définir la propriété facultative d’un contrôle de la façon dont le contenu de texte de votre [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) `message` message est rendu. Voir [la mise en forme des messages](~/resources/bot-v3/bots-message-format.md) pour obtenir une description détaillée de la mise en forme prise en charge dans les messages du bot.
Vous pouvez définir la propriété facultative pour contrôler le rendu du contenu du [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) texte de votre message.

Pour plus d’informations sur la façon dont Teams prend en charge la mise en forme du texte dans les équipes, voir La mise en forme du texte [dans les messages du bot.](~/resources/bot-v3/bots-text-formats.md)

Pour plus d’informations sur la mise en forme des cartes dans les messages, voir [Mise en forme de carte.](~/task-modules-and-cards/cards/cards-format.md)

## <a name="picture-messages"></a>Messages image

Les images sont envoyées en ajoutant des pièces jointes à un message. Vous trouverez plus d’informations sur les pièces jointes dans la [documentation bot Framework.](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)

Les images peuvent être au maximum 1024×1024 et 1 Mo au format PNG, JPEG ou GIF ; Gif animé non pris en charge.

Nous vous recommandons de spécifier la hauteur et la largeur de chaque image à l’aide de XML. Si vous utilisez Markdown, la taille par défaut de l’image est 256×256. Par exemple :

* Utiliser `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Ne pas utiliser `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Réception de messages

Selon les étendues déclarées, votre bot peut recevoir des messages dans les contextes suivants :

* **conversation personnelle** Les utilisateurs peuvent interagir dans une conversation privée avec un bot en sélectionnant simplement le bot ajouté dans l’historique de conversation ou en tapant son nom ou son ID d’application dans la zone À : d’une nouvelle conversation.
* **Canaux** Un bot peut être mentionné (« @_botname_») dans un canal s’il a été ajouté à l’équipe. Notez que les réponses supplémentaires à un bot dans un canal nécessitent de mentionner le bot. Il ne répond pas aux réponses lorsqu’il n’est pas mentionné.

Pour les messages entrants, votre bot reçoit un objet [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) de type `messageType: message` . Bien que l’objet puisse contenir d’autres types d’informations, tels que les mises à jour de canal envoyées à votre bot, le type représente la `Activity` communication entre le bot et [](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` l’utilisateur.

Votre bot reçoit une charge utile qui contient le message de l’utilisateur, ainsi que d’autres informations sur l’utilisateur, la source du message et `Text` Teams informations. Remarque :

* `timestamp` Date et heure du message en temps universel coordonné (UTC).
* `localTimestamp` Date et heure du message dans le fuseau horaire de l’expéditeur.
* `channelId` Toujours « msteams ». Il s’agit d’un canal d’infrastructure de bot, et non d’un canal d’équipes.
* `from.id` Un ID unique et chiffré pour cet utilisateur pour votre bot ; convient comme clé si votre application doit stocker des données utilisateur. Il est unique pour votre bot et ne peut pas être directement utilisé en dehors de votre instance de bot d’une manière significative pour identifier cet utilisateur.
* `channelData.tenant.id` ID de locataire de l’utilisateur.

> [!NOTE]
> `from.id` est unique pour votre bot et ne peut pas être directement utilisé en dehors de votre instance de bot d’une manière significative pour identifier cet utilisateur.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Combinaison d’interactions canal et privée avec votre bot

Lorsque vous interagissez dans un canal, votre bot doit être intelligent pour mettre certaines conversations hors connexion avec un utilisateur. Par exemple, supposons qu’un utilisateur tente de coordonner une tâche complexe, telle que la planification avec un ensemble de membres de l’équipe. Plutôt que d’avoir toute la séquence d’interactions visible pour le canal, envisagez d’envoyer un message de conversation personnelle à l’utilisateur. Votre bot doit pouvoir facilement faire passer l’utilisateur entre les conversations personnelles et les conversations de canal sans perte d’état.

> [!NOTE]
>N’oubliez pas de mettre à jour le canal lorsque l’interaction est terminée pour en informer les autres membres de l’équipe.

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
> Le champ de texte pour les messages entrants contient parfois des mentions. Assurez-vous de les vérifier et de les bander correctement. Pour plus d’informations, voir [Mentions.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)

## <a name="teams-channel-data"></a>Teams canal de distribution

L’objet contient des Teams spécifiques et constitue la source définitive des ID d’équipe et `channelData` de canal. Vous devez mettre en cache et utiliser ces ID comme clés pour le stockage local.

L’objet n’est pas inclus dans les messages dans les conversations personnelles, car ils ont lieu en `channelData` dehors d’un canal.

Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :

* `eventType`Teams type d’événement ; transmis uniquement en cas d’événements [de modification de canal.](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id`Azure Active Directory ID de client ; transmis dans tous les contextes.
* `team` Transmis uniquement dans les contextes de canal, et non dans la conversation personnelle.
  * `id` GUID du canal.
  * `name`Nom de l’équipe ; transmis uniquement dans les cas d’événements [de changement de nom d’équipe.](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel` Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour les événements dans les canaux dans les équipes où le bot a été ajouté.
  * `id` GUID du canal.
  * `name`Nom du canal ; transmis uniquement en cas d’événements [de modification de canal.](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `channelData.teamsTeamId` Deprecated. Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.
* `channelData.teamsChannelId` Deprecated. Cette propriété est incluse uniquement pour des raisons de compatibilité ascendante.

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

Le package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet fournit un objet spécialisé, qui expose les propriétés pour accéder Teams `TeamsChannelData` des informations spécifiques.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Envoi de réponses aux messages

Pour répondre à un message existant, [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) appelez .NET ou [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) dans Node.js. Le SDK Bot Builder gère tous les détails.

Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) point de terminaison.

Le contenu du message lui-même peut contenir du texte simple ou certaines des cartes et [actions](~/task-modules-and-cards/cards/cards-actions.md)de carte fournies par Bot Framework.

Notez que dans votre schéma sortant, vous devez toujours utiliser le même schéma que celui `serviceUrl` que vous avez reçu. N’ignorez pas que la valeur `serviceUrl` tend à être stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée de `serviceUrl` .

## <a name="updating-messages"></a>Mise à jour des messages

Au lieu que vos messages soient des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages en ligne après les avoir envoyés. Vous pouvez utiliser les mises à jour dynamiques des messages pour des scénarios tels que les mises à jour des sondages, la modification des actions disponibles après une pression sur un bouton ou tout autre changement d’état asynchrone.

Le nouveau message ne doit pas nécessairement correspondre au type d’origine. Par exemple, si le message d’origine contenait une pièce jointe, le nouveau message peut être un message texte simple.

> [!NOTE]
> Vous pouvez mettre à jour uniquement le contenu envoyé dans les messages à pièce jointe unique et les dispositions de carrousels. La publication de mises à jour dans des messages avec plusieurs pièces jointes dans la mise en page de liste n’est pas prise en charge.

### <a name="rest-api"></a>API REST

Pour émettre une mise à jour de message, effectuez simplement une requête PUT sur le point de terminaison à `/v3/conversations/<conversationId>/activities/<activityId>/` l’aide d’un ID d’activité donné. Pour terminer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel POST d’origine.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Exemple .NET

Vous pouvez utiliser la `UpdateActivityAsync` méthode dans le SDK Bot Builder pour mettre à jour un message existant.

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

### <a name="nodejs-example"></a>Node.js exemple

Vous pouvez utiliser la `session.connector.update` méthode dans le SDK Bot Builder pour mettre à jour un message existant.

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

Vous pouvez créer une conversation personnelle avec un utilisateur ou démarrer une nouvelle chaîne de réponse dans un canal pour votre bot d’équipe. Cela vous permet d’envoyer un message à vos utilisateurs sans qu’ils contactent d’abord votre bot. Pour plus d’informations, voir les rubriques suivantes :

Pour [plus d’informations générales](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) sur les conversations démarrées par les bots, voir messagerie proactive pour les bots.

## <a name="deleting-messages"></a>Suppression de messages

Les messages peuvent être supprimés à l’aide de la méthode connecteurs dans [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) le [SDK BotBuilder](/bot-framework/bot-builder-overview-getstarted).

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
