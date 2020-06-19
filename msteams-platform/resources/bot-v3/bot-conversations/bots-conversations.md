---
title: Envoyer et recevoir des messages avec un bot
description: Indique comment envoyer et recevoir des messages avec des robots dans Microsoft teams
keywords: messages des robots teams
ms.date: 05/20/2019
ms.openlocfilehash: 4a15bb9b4ae8c0ede3214d3a534649e2769baf6e
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "44801134"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Avoir une conversation avec un robot Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs. Il existe trois types de conversations (ou portées) dans Teams :

* `teams`Également appelés conversations de canal, visibles par tous les membres du canal.
* `personal`Les conversations entre les robots et un seul utilisateur.
* `groupChat`Conversation entre un bot et deux utilisateurs ou plus.

Un bot se comporte de manière légèrement différente en fonction du type de conversation impliquée :

* Les [robots dans les conversations de conversation de groupe et de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) exigent que l’utilisateur appelle le robot pour l’appeler dans un canal.
* Les [robots dans les conversations avec un seul utilisateur](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) ne nécessitent pas de @ mentions-l’utilisateur peut simplement taper.

Pour que le bot fonctionne dans une étendue particulière, il doit être indiqué comme étant pris en charge par cette étendue dans le manifeste. Les étendues sont définies et décrites plus en détail dans la [référence de manifeste](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Messages proactifs

Les robots peuvent participer à une conversation ou initier une conversation. La plupart des communications sont en réponse à un autre message. Si un bot lance une conversation, il s’appelle un *message proactif*. Exemples :

* Les messages de bienvenue
* Notifications d’événements
* Interrogation des messages

## <a name="conversation-basics"></a>Concepts de base d’une conversation

Chaque message est un objet `Activity` de type `messageType: message`. Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot. Votre bot examine le message pour déterminer son type et répond en conséquence.

Les robots prennent également en charge les messages de style événement. Pour plus d’informations, voir [gérer les événements bot dans Microsoft teams](~/resources/bot-v3/bots-notifications.md) . La reconnaissance vocale n’est pas prise en charge actuellement.

Les messages sont en grande partie identiques pour toutes les étendues, mais il existe des différences entre l’accès au bot dans l’interface utilisateur et les différences par rapport aux scènes que vous devrez connaître.

La conversation de base est gérée via le connecteur de l’infrastructure bot, une seule API REST pour permettre à votre bot de communiquer avec teams et d’autres canaux. Le kit de développement logiciel (SDK) du générateur de robots offre un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux de conversation et l’État, et des méthodes simples pour incorporer des services cognitifs tels que le traitement du langage naturel (NLP).

## <a name="message-content"></a>Contenu du message

Votre robot peut envoyer du texte enrichi, des images et des cartes. Les utilisateurs peuvent envoyer du texte enrichi et des images à votre bot. Vous pouvez spécifier le type de contenu que votre robot peut gérer dans la page Paramètres de Microsoft teams de votre robot.

| Format | De l’utilisateur au bot  | Du bot à l’utilisateur |  Notes |
| --- | :---: | :---: | --- |
| Texte enrichi  | ✔ | ✔ |  |
| Images | ✔ | ✔ | Taille maximale 1024 x 1024 et 1 Mo au format PNG, JPEG ou GIF ; les images GIF animées ne sont pas prises en charge |
| Cartes | ✖ | ✔ | Voir la [référence de la carte teams](~/task-modules-and-cards/cards/cards-reference.md) pour les cartes prises en charge |
| Emojis | ✖ | ✔ | Teams prend actuellement en charge les Emoji via UTF-16 (par exemple, U + 1F600 pour Grinning face) |
|

Pour plus d’informations sur les types d’interaction des robots pris en charge par l’infrastructure bot (quels sont les robots en équipe), voir la documentation de l’infrastructure de robot sur le [flux de conversation](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) et les concepts connexes dans la documentation du kit de développement logiciel (SDK) du [Générateur de robots pour .net](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) et [le kit de développement logiciel (SDK) du générateur de robots pour Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).

## <a name="message-formatting"></a>Mise en forme de messages

Vous pouvez définir la [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) propriété facultative d’un `message` pour contrôler le mode d’affichage du contenu de texte de votre message. Consultez la rubrique [mise en forme](~/resources/bot-v3/bots-message-format.md) des messages pour une description détaillée de la mise en forme prise en charge dans les messages bot.
Vous pouvez définir la propriété Optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) pour contrôler le rendu du contenu de texte de votre message.

Pour plus d’informations sur la façon dont teams prend en charge la mise en forme de texte dans Teams, consultez la rubrique [formatage du texte dans les messages bot](~/resources/bot-v3/bots-text-formats.md)

Pour plus d’informations sur la mise en forme des cartes dans les messages, voir [Card Formatting](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Messages d’image

Les images sont envoyées par l’ajout de pièces jointes à un message. Vous trouverez plus d’informations sur les pièces jointes dans la documentation de l' [infrastructure bot](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).

Les images peuvent être d’au moins 1024 × 1024 et 1 Mo au format PNG, JPEG ou GIF ; l’image GIF animée n’est pas prise en charge.

Nous vous recommandons de spécifier la hauteur et la largeur de chaque image à l’aide de XML. Si vous utilisez la démarque, la taille de l’image est par défaut de 256 × 256. Par exemple :

* Utilisant`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* Ne pas utiliser`![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Réception de messages

Selon les étendues déclarées, votre robot peut recevoir des messages dans les contextes suivants :

* **conversation personnelle** Les utilisateurs peuvent interagir dans une conversation privée avec un bot en sélectionnant simplement le bot ajouté dans l’historique de la conversation ou en tapant son nom ou son ID d’application dans la zone à : d’une nouvelle conversation.
* **Canaux** Un bot peut être mentionné (« @_botname_») dans un canal s’il a été ajouté à l’équipe. Notez que les réponses supplémentaires à un bot dans un canal nécessitent de mentionner le bot. Il ne répond pas aux réponses qui ne sont pas mentionnées.

Pour les messages entrants, votre bot reçoit un [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) objet de type `messageType: message` . Bien que l' `Activity` objet puisse contenir d’autres types d’informations, comme les [mises à jour de canal](~/resources/bot-v3/bots-notifications.md#channel-updates) envoyées à votre bot, le `message` type représente la communication entre le bot et l’utilisateur.

Votre bot reçoit une charge qui contient le message de l’utilisateur `Text` ainsi que d’autres informations sur l’utilisateur, la source du message et des informations sur les équipes. De note :

* `timestamp`Date et heure du message en temps universel coordonné (UTC)
* `localTimestamp`Date et heure du message dans le fuseau horaire de l’expéditeur
* `channelId`Toujours « msteams ». Cela fait référence à un canal d’infrastructure bot, pas à un canal Teams.
* `from.id`Un ID unique et chiffré pour cet utilisateur pour votre bot ; Cette clé est appropriée si votre application a besoin de stocker des données utilisateur. Il est unique pour votre robot et ne peut pas être directement utilisé en dehors de votre instance de robot de manière significative pour identifier cet utilisateur
* `channelData.tenant.id`ID de client de l’utilisateur.

> [!NOTE]
> `from.id`est unique pour votre bot et ne peut pas être directement utilisé en dehors de votre instance de robot de manière significative pour identifier cet utilisateur.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Combinaison d’interactions de canal et de privé avec votre robot

Lors de l’interaction dans un canal, votre robot doit être intelligent quant à la prise en main de certaines conversations avec un utilisateur. Par exemple, supposons qu’un utilisateur tente de coordonner une tâche complexe, telle que la planification d’un ensemble de membres d’équipe. Au lieu d’avoir l’intégralité de la séquence d’interactions visible par le canal, envisagez d’envoyer un message de conversation personnelle à l’utilisateur. Votre robot doit être en mesure de transférer facilement l’utilisateur entre les conversations personnelles et les conversations de canal sans perte d’État.

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
> Le champ de texte pour les messages entrants contient parfois des mentions. Assurez-vous de vérifier et de les supprimer correctement. Pour plus d’informations, consultez la rubrique [mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>Données de canal teams

L' `channelData` objet contient des informations spécifiques aux équipes et constitue la source définitive des ID d’équipe et de canal. Vous devez mettre en cache et utiliser ces ID en tant que clés pour le stockage local.

L' `channelData` objet n’est pas inclus dans les messages dans les conversations personnelles, étant donné qu’ils ont lieu en dehors de n’importe quel canal.

Un objet channelData classique dans une activité envoyée à votre bot contient les informations suivantes :

* `eventType`Type d’événement teams ; transmis uniquement en cas d' [événements de modification de canal](~/resources/bot-v3/bots-notifications.md#channel-updates)
* `tenant.id`ID de locataire Azure Active Directory ; transmis dans tous les contextes
* `team`Transmis uniquement dans les contextes de canal, pas dans la conversation personnelle.
  * `id`GUID du canal
  * `name`Nom de l’équipe ; transmis uniquement en cas d' [événement de changement de nom d’équipe](~/resources/bot-v3/bots-notifications.md#team-name-updates)
* `channel`Transmis uniquement dans les contextes de canal lorsque le bot est mentionné ou pour des événements dans des canaux dans teams où le bot a été ajouté
  * `id`GUID du canal
  * `name`Nom du canal ; transmis uniquement en cas d' [événements de modification de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `channelData.teamsTeamId`Déconseillées. Cette propriété est incluse uniquement à des fins de compatibilité descendante.
* `channelData.teamsChannelId`Déconseillées. Cette propriété est incluse uniquement à des fins de compatibilité descendante.

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

Le package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) fournit un `TeamsChannelData` objet spécialisé, qui expose les propriétés permettant d’accéder aux informations spécifiques aux équipes.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Envoi de réponses à des messages

Pour répondre à un message existant, appelez [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) en .net ou [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) dans Node.js. Le kit de développement logiciel (SDK) du générateur de robots gère tous les détails.

Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) point de terminaison.

Le contenu du message lui-même peut contenir du texte simple ou une partie des [cartes et des actions de carte](~/task-modules-and-cards/cards/cards-actions.md)fournis.

Veuillez noter que dans votre schéma sortant, vous devez toujours utiliser le même `serviceUrl` que celui que vous avez reçu. N’oubliez pas que la valeur de `serviceUrl` tend à être stable mais peut varier. Lors de l’arrivée d’un nouveau message, votre robot doit vérifier sa valeur stockée `serviceUrl` .

## <a name="updating-messages"></a>Mise à jour des messages

Au lieu de faire en sorte que vos messages soient des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages insérés après les avoir envoyés. Vous pouvez utiliser les mises à jour de messages dynamiques pour des scénarios tels que les mises à jour de sondage, la modification des actions disponibles après une pression sur un bouton ou tout autre changement d’état asynchrone.

Le nouveau message n’a pas besoin de correspondre au type d’origine. Par exemple, si le message d’origine contient une pièce jointe, le nouveau message peut être un simple message texte.

> [!NOTE]
> Vous pouvez mettre à jour uniquement le contenu envoyé dans les mises en page et les messages à une seule pièce jointe. La publication de mises à jour de messages avec plusieurs pièces jointes dans la mise en forme de liste n’est pas prise en charge.

### <a name="rest-api"></a>API REST

Pour émettre une mise à jour de message, effectuez simplement une requête PUT sur le `/v3/conversations/<conversationId>/activities/<activityId>/` point de terminaison à l’aide d’un ID d’activité donné. Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel POST d’origine.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Exemple .NET

Vous pouvez utiliser la `UpdateActivityAsync` méthode dans le kit de développement logiciel (SDK) du générateur de robots pour mettre à jour un message existant.

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

### <a name="nodejs-example"></a>Exemple de Node.js

Vous pouvez utiliser la `session.connector.update` méthode dans le kit de développement logiciel (SDK) du générateur de robots pour mettre à jour un message existant.

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

Vous pouvez créer une conversation personnelle avec un utilisateur ou démarrer une nouvelle chaîne de réponse dans un canal pour votre robot d’équipe. Cela vous permet d’envoyer un message à votre utilisateur ou à vos utilisateurs sans qu’ils commencent par contacter le robot. Pour plus d’informations, voir les rubriques suivantes :

Consultez la rubrique [messagerie proactive pour les robots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) pour obtenir des informations plus générales sur les conversations démarrées par les robots.

## <a name="deleting-messages"></a>Suppression de messages

Les messages peuvent être supprimés à l’aide de la [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) méthode Connectors dans le [Kit de développement logiciel (SDK) BotBuilder](/bot-framework/bot-builder-overview-getstarted).

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
