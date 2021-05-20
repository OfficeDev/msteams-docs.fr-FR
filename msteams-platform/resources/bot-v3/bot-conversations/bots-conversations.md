---
title: Envoyer et recevoir des messages avec un bot
description: Décrit comment envoyer et recevoir des messages avec des bots dans Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: équipes bots messages
ms.date: 05/20/2019
ms.openlocfilehash: e1926afe42bca45eda5f39be1be8342452b3aa24
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566494"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>Avoir une conversation avec un bot Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Une conversation est une série de messages échangés entre votre bot et un ou plusieurs utilisateurs. Il existe trois types de conversations (ou portées) dans Teams :

* `teams` Aussi appelé conversations de canal, visible à tous les membres de la chaîne.
* `personal` Conversations entre les bots et un seul utilisateur.
* `groupChat` Discutez entre un bot et deux utilisateurs ou plus.

Un bot se comporte légèrement différemment selon le type de conversation dans qui il est impliqué :

* [Les bots dans les conversations de chat de canal et de](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) groupe exigent que l’utilisateur @mention le bot pour l’invoquer dans un canal.
* [Les bots dans les conversations utilisateur](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) unique ne nécessitent pas de @mention - l’utilisateur peut simplement taper.

Pour que le bot fonctionne dans une portée particulière, il doit être répertorié comme soutenant cette portée dans le manifeste. Les portées sont définies et examinées plus en détail dans [la référence manifeste](~/resources/schema/manifest-schema.md).

## <a name="proactive-messages"></a>Messages proactifs

Les bots peuvent participer à une conversation ou en initier une. La plupart des communications sont en réponse à un autre message. Si un bot lance une conversation, il s’appelle un *message proactif*. Par exemple :

* Les messages de bienvenue
* Notifications d’événements
* Messages de sondage

## <a name="conversation-basics"></a>Concepts de base d’une conversation

Chaque message est un objet `Activity` de type `messageType: message`. Lorsqu’un utilisateur envoie un message, Teams le publie sur votre bot. Plus précisément, il envoie un objet JSON au point de terminaison de messagerie de votre bot. Votre bot examine le message pour déterminer son type et répond en conséquence.

Les bots soutiennent également les messages de style événement. Pour plus d’informations, [voir Gérer les événements bot dans Microsoft Teams](~/resources/bot-v3/bots-notifications.md). Le discours n’est actuellement pas pris en charge.

Les messages sont pour la plupart les mêmes dans toutes les étendues, mais il ya des différences dans la façon dont le bot est accessible dans l’interface utilisateur et les différences dans les coulisses que vous aurez besoin de connaître.

La conversation de base est traitée via le connecteur Bot Framework, une seule API REST pour permettre à votre bot de communiquer avec les Teams et d’autres canaux. Le Bot Builder SDK offre un accès facile à cette API, des fonctionnalités supplémentaires pour gérer le flux de conversation et l’état, et des moyens simples d’intégrer des services cognitifs tels que le traitement du langage naturel (NLP).

## <a name="message-content"></a>Contenu du message

Votre bot peut envoyer du texte riche, des photos et des cartes. Les utilisateurs peuvent envoyer du texte et des images riches à votre bot. Vous pouvez spécifier le type de contenu que votre bot peut gérer dans la page Microsoft Teams paramètres de votre bot.

| Format | De l’utilisateur au bot  | Du bot à l’utilisateur |  Remarques |
| --- | :---: | :---: | --- |
| Texte enrichi  | ✔ | ✔ |  |
| Images | ✔ | ✔ | Maximum 1024×1024 et 1 Mo en format PNG, JPEG ou GIF; gif animé ne sont pas pris en charge. |
| Cartes | ✖ | ✔ | Consultez la référence [Teams carte pour les](~/task-modules-and-cards/cards/cards-reference.md) cartes prises en charge. |
| Emojis | ✖ | ✔ | Teams supporte actuellement les emojis via UTF-16 tels que U+1F600 pour le visage souriant. |
|

Pour plus d’informations sur les types d’interaction bot pris en charge par le Bot Framework, sur lequel les bots en équipes sont basés, consultez la documentation Bot Framework sur [le flux de conversation](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) et les concepts connexes dans la documentation pour le Bot Builder [SDK pour .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) [et le Bot Builder SDK pour Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).

## <a name="message-formatting"></a>Mise en forme de messages

Vous pouvez définir la propriété [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) optionnelle `message` d’un pour contrôler la façon dont le contenu texte de votre message est rendu. Voir [formatage de message](~/resources/bot-v3/bots-message-format.md) pour une description détaillée du formatage pris en charge dans les messages bot.
Vous pouvez définir la propriété [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) optionnelle pour contrôler la façon dont le contenu texte de votre message est rendu.

Pour plus d’informations sur la façon dont Teams prend en charge le formatage du texte dans les équipes [voir formatage de texte dans les messages bot](~/resources/bot-v3/bots-text-formats.md).

Pour plus d’informations sur le formatage des cartes dans les messages, [voir Formatage de la carte](~/task-modules-and-cards/cards/cards-format.md).

## <a name="picture-messages"></a>Messages d’image

Les images sont envoyées en ajoutant des pièces jointes à un message. Vous pouvez trouver plus d’informations sur les pièces jointes dans [la documentation Bot Framework](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).

Les images peuvent être tout au plus 1024×1024 et 1 Mo en format PNG, JPEG ou GIF; GIF animé n’est pas pris en charge.

Nous vous recommandons de spécifier la hauteur et la largeur de chaque image en utilisant XML. Si vous utilisez Markdown, la taille de l’image est par défaut à 256×256. Par exemple :

* Utiliser `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* N’utilisez pas `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>Réception de messages

Selon les étendues déclarées, votre bot peut recevoir des messages dans les contextes suivants :

* **chat personnel** Les utilisateurs peuvent interagir dans une conversation privée avec un bot en sélectionnant simplement le bot ajouté dans l’historique du chat, ou en tapant son nom ou son identifiant d’application dans le To: box sur un nouveau chat.
* **Canaux** Un bot peut être mentionné (« @_botname_« ) dans un canal s’il a été ajouté à l’équipe. Notez que les réponses supplémentaires à un bot dans un canal nécessitent de mentionner le bot. Il ne répondra pas aux réponses lorsqu’il n’est pas mentionné.

Pour les messages entrants, votre bot reçoit [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) un objet de type `messageType: message` . Bien que `Activity` l’objet puisse contenir d’autres types d’informations, comme [les mises à jour](~/resources/bot-v3/bots-notifications.md#channel-updates) de canaux envoyées à votre bot, le type représente la communication entre le bot et `message` l’utilisateur.

Votre bot reçoit une charge utile qui contient le message de `Text` l’utilisateur ainsi que d’autres informations sur l’utilisateur, la source du message et Teams informations. important:

* `timestamp` La date et l’heure du message dans Le Temps Universel Coordonné (UTC).
* `localTimestamp` La date et l’heure du message dans le fuseau horaire de l’expéditeur.
* `channelId` Toujours « msteams ». Il s’agit d’un canal-cadre bot, pas d’un canal d’équipes.
* `from.id` Un iD unique et crypté pour cet utilisateur pour votre bot; comme clé si votre application a besoin de stocker des données utilisateur. Il est unique pour votre bot et ne peut pas être directement utilisé en dehors de votre instance bot d’une manière significative pour identifier cet utilisateur.
* `channelData.tenant.id` L’iD du locataire pour l’utilisateur.

> [!NOTE]
> `from.id` est unique pour votre bot et ne peut pas être directement utilisé en dehors de votre instance bot de quelque manière significative pour identifier cet utilisateur.

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>Combiner les interactions canal et privées avec votre bot

Lorsque vous interagissez dans un canal, votre bot doit être intelligent pour mettre certaines conversations hors ligne avec un utilisateur. Par exemple, supposons qu’un utilisateur essaie de coordonner une tâche complexe, comme la planification avec un ensemble de membres de l’équipe. Plutôt que d’avoir toute la séquence d’interactions visibles sur le canal, envisagez d’envoyer un message de chat personnel à l’utilisateur. Votre bot devrait être en mesure de faire la transition facile de l’utilisateur entre les conversations personnelles et de canal sans perdre l’état.

> [!NOTE]
>N’oubliez pas de mettre à jour le canal lorsque l’interaction est terminée pour aviser les autres membres de l’équipe.

## <a name="full-inbound-schema-example"></a>Exemple complet de schéma entrant

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
> Le champ texte pour les messages entrants contient parfois des mentions. Assurez-vous de bien les vérifier et de les dépouiller. Pour plus d’informations, voir [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).

## <a name="teams-channel-data"></a>Teams de canal

`channelData`L’objet contient Teams informations spécifiques et est la source définitive pour les iD d’équipe et de canal. Vous devez mettre en cache et utiliser ces ids comme clés pour le stockage local.

`channelData`L’objet n’est pas inclus dans les messages dans les conversations personnelles puisque ceux-ci ont lieu en dehors de n’importe quel canal.

Un objet canalData typique dans une activité envoyée à votre bot contient les informations suivantes :

* `eventType`Teams type d’événement; passé seulement en cas d’événements [de modification de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `tenant.id`Azure Active Directory d’identité du locataire; passé dans tous les contextes.
* `team` Passé uniquement dans les contextes de canaux, pas dans le chat personnel.
  * `id` GUID pour la chaîne.
  * `name` Nom de l’équipe; passé seulement dans les cas d’équipe [renommer les événements](~/resources/bot-v3/bots-notifications.md#team-name-updates).
* `channel` Passé uniquement dans les contextes de canaux lorsque le bot est mentionné ou pour des événements dans les canaux dans les équipes où le bot a été ajouté.
  * `id` GUID pour la chaîne.
  * `name` Nom de la chaîne; passé seulement en cas d’événements [de modification de canal](~/resources/bot-v3/bots-notifications.md#channel-updates).
* `channelData.teamsTeamId` obsolescent. Cette propriété est incluse uniquement pour la compatibilité vers l’arrière.
* `channelData.teamsChannelId` obsolescent. Cette propriété est incluse uniquement pour la compatibilité vers l’arrière.

### <a name="example-channeldata-object-channelcreated-event"></a>Exemple d’objet channelData (événement canalCréé)

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

Le [package Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet fournit un objet `TeamsChannelData` spécialisé, qui expose les propriétés pour accéder à des informations Teams spécifiques.

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>Envoi de réponses aux messages

Pour répondre à un message existant, [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) appelez .NET ou [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) en Node.js. Le Bot Builder SDK gère tous les détails.

Si vous choisissez d’utiliser l’API REST, vous pouvez également appeler le point [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) de terminaison.

Le contenu du message lui-même peut contenir du texte simple ou certaines des cartes fournies par Bot Framework [et des actions de carte.](~/task-modules-and-cards/cards/cards-actions.md)

Veuillez noter que dans votre schéma sortant, vous devez toujours utiliser le même que `serviceUrl` celui que vous avez reçu. Sachez que la valeur de tend `serviceUrl` à être stable, mais peut changer. Lorsqu’un nouveau message arrive, votre bot doit vérifier sa valeur stockée de `serviceUrl` .

## <a name="updating-messages"></a>Mise à jour des messages

Plutôt que d’avoir vos messages être des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages en ligne après les avoir envoyés. Vous pouvez utiliser des mises à jour de messages dynamiques pour des scénarios tels que les mises à jour de sondage, la modification des actions disponibles après une pression sur le bouton ou tout autre changement d’état asynchrone.

Le nouveau message n’a pas besoin de correspondre à l’original dans le type. Par exemple, si le message original contenait une pièce jointe, le nouveau message peut être un simple message texte.

> [!NOTE]
> Vous ne pouvez mettre à jour que le contenu envoyé dans les messages à pièce jointe unique et les mises en page carrousel. L’affichage de mises à jour de messages avec plusieurs pièces jointes dans la mise en page de liste n’est pas pris en charge.

### <a name="rest-api"></a>API REST

Pour émettre une mise à jour de message, il vous suffit d’exécuter une demande PUT par rapport au point `/v3/conversations/<conversationId>/activities/<activityId>/` de terminaison à l’aide d’un ID d’activité donné. Pour compléter ce scénario, vous devez mettre en cache l’ID d’activité retourné par l’appel POST d’origine.

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>Exemple .NET

Vous pouvez utiliser la méthode `UpdateActivityAsync` dans le Bot Builder SDK pour mettre à jour un message existant.

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

Vous pouvez utiliser la méthode `session.connector.update` dans le Bot Builder SDK pour mettre à jour un message existant.

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

Vous pouvez créer une conversation personnelle avec un utilisateur ou démarrer une nouvelle chaîne de réponse dans un canal pour votre bot d’équipe. Cela vous permet de messager à votre utilisateur ou utilisateurs sans les avoir d’abord initier le contact avec votre bot. Pour plus d’informations, voir les rubriques suivantes :

Consultez [la messagerie proactive pour les bots pour](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) plus d’informations générales sur les conversations lancées par les bots.

## <a name="deleting-messages"></a>Suppression des messages

Les messages peuvent être supprimés en utilisant la [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) méthode des connecteurs [dans le BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).

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
