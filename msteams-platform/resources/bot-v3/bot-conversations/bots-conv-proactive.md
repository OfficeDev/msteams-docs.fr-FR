---
title: Messagerie proactive pour les bots
description: Dans ce module, découvrez comment utiliser la messagerie proactive pour les bots et les meilleures pratiques pour la messagerie proactive dans Microsoft Teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: ee193cd7dfcfec20f501483eabc3a485cff0caab
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143129"
---
# <a name="proactive-messaging-for-bots"></a>Messagerie proactive pour les bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un message proactif est un message envoyé par un bot pour démarrer une conversation. Vous voudrez peut-être que votre bot démarre une conversation pour diverses raisons, notamment :

* Messages de bienvenue pour les conversations de bot personnel.
* Réponses aux sondages.
* Notifications d’événements externes.
L’envoi d’un message pour démarrer un nouveau thread de conversation est différent de l’envoi d’un message en réponse à une conversation existante : lorsque votre bot démarre une nouvelle conversation, il n’existe aucune conversation préexistante à laquelle publier le message. Pour envoyer un message proactif, vous devez :

1. [Décidez de ce que vous allez dire](#best-practices-for-proactive-messaging)
1. [Obtenir l’ID unique et l’ID de locataire de l’utilisateur](#obtain-necessary-user-information)
1. [Envoyer le message](#examples)

Lorsque vous créez des messages proactifs, vous **devez** appeler `MicrosoftAppCredentials.TrustServiceUrl`et transmettre l’URL du service avant de créer le `ConnectorClient` utilisé pour envoyer le message. Si ce n’est pas le cas, une réponse `401: Unauthorized` est reçue par votre application. Pour plus d’informations, consultez [les exemples ci-dessous](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques en matière de messagerie proactive

L’envoi de messages proactifs est un moyen efficace de communiquer avec vos utilisateurs. Toutefois, du point de vue des utilisateurs, le message s’affiche de manière spontanée. Lorsqu’il y a un message de bienvenue, il s’agira de leur première interaction avec votre application. Il est important d’utiliser cette fonctionnalité et de fournir des informations complètes à l’utilisateur pour comprendre l’objectif de ce message.

Les messages proactifs sont généralement classés en deux catégories : les messages de bienvenue ou les messages de notification.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lorsque vous utilisez la messagerie proactive pour envoyer un message d’accueil à un utilisateur, assurez-vous que, du point de vue de l’utilisateur, le message semble non traité. Lorsqu’il y a un message de bienvenue, il s’agira de leur première interaction avec votre application. Les meilleurs messages d’accueil sont les suivants :

* **Pourquoi ils reçoivent ce message**: il doit être clair pour l’utilisateur pourquoi il reçoit ce message. Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, indiquez-leur dans quel canal il a été installé et éventuellement qui l’a installé.
* **Que proposez-vous**: que peuvent-ils faire avec votre application ? Quelle valeur pouvez-vous leur apporter ?
* **Que doivent-ils faire ensuite**: invitez-les à essayer une commande ou à interagir avec votre application d’une certaine manière.

### <a name="notification-messages"></a>Les messages de notification

Lorsque vous utilisez la messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs disposent d'un chemin clair pour effectuer les actions courantes basées sur votre notification, et qu'ils comprennent clairement pourquoi la notification s'est produite. Les bons messages de notification comprennent généralement les éléments suivants

* **Ce qui s’est passé**: une indication claire de la cause de la notification.
* **Ce qui est arrivé à** : Il doit être clair quel élément/chose a été mis à jour pour provoquer la notification.
* **Qui l'a fait** : Qui a pris l'action qui a provoqué l'envoi de la notification ?
* **ce qu’ils peuvent faire**: facilitez la prise d’actions par vos utilisateurs en fonction de vos notifications.
* **comment ils peuvent refuser**: indiquez un chemin d’accès permettant aux utilisateurs de refuser des notifications supplémentaires.

## <a name="obtain-necessary-user-information"></a>Obtenir les informations utilisateur nécessaires

Les bots peuvent créer des conversations avec un utilisateur Microsoft Teams individuel en obtenant *l’ID unique de l’utilisateur* et *l’ID de locataire*. Vous pouvez obtenir ces valeurs à l’aide de l’une des méthodes suivantes :

* En [récupérant la liste d’équipe](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) à partir d’un canal, votre application est installée.
* En les mettant en cache lorsqu’un utilisateur [interagit avec votre bot dans un canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).
* Lorsqu’un utilisateur est [@mentioned dans une conversation de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) le bot fait partie de.
* En les mettant en cache lorsque vous [recevoir l’événement `conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) lorsque votre application est installée dans une étendue personnelle, ou que de nouveaux membres sont ajoutés à un canal ou à une conversation de groupe qui s’y ajoute.

### <a name="proactively-install-your-app-using-graph"></a>Installer votre application de manière proactive en utilisant Graph

> [!Note]
> L’installation proactive d’applications à l’aide de Graph est actuellement en version bêta.

Parfois, il peut être nécessaire d’envoyer des messages proactifs aux utilisateurs qui n’ont pas déjà installé ou interagi avec votre application. Par exemple, vous souhaitez utiliser le [communicateur d’entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’échelle de votre organisation. Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir du `conversationUpdate` événement que votre application recevra lors de l’installation.

Vous pouvez uniquement installer des applications qui se trouvent dans votre catalogue d’applications d’organisation ou dans l’App Store Teams.

Pour plus d’informations, consultez [Installer des applications pour les utilisateurs](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true) dans la documentation Graph. Il existe également un [exemple dans .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Exemples

Veillez à vous authentifier et à disposer d’un jeton de porteur avant de créer une conversation à l’aide de l’API REST.

```json
POST /v3/conversations
{
  "bot": {
    "id": "28:10j12ou0d812-2o1098-c1mjojzldxcj-1098028n ",
    "name": "The Bot"
  },
  "members": [
    {
      "id": "29:012d20j1cjo20211"
    }
  ],
  "channelData": {
    "tenant": {
      "id": "197231joe-1209j01821-012kdjoj"
    }
  }
}
```

Vous devez fournir l’identifiant utilisateur et l’identifiant du client. Si l’appel réussit, l’API retourne l’objet de réponse suivant.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Cet ID est l’ID de conversation unique de la conversation personnelle. Stockez cette valeur et réutilisez-la pour les interactions futures avec l’utilisateur.

### <a name="using-net"></a>Utilisation de .NET

Cet exemple utilise le package NuGet [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams).

```csharp
// Create or get existing chat conversation with user
var response = client.Conversations.CreateOrGetDirectConversation(activity.Recipient, activity.From, activity.GetTenantId());

// Construct the message to post to conversation
Activity newActivity = new Activity()
{
    Text = "Hello",
    Type = ActivityTypes.Message,
    Conversation = new ConversationAccount
    {
        Id = response.Id
    },
};

// Post the message to chat conversation with user
await client.Conversations.SendToConversationAsync(newActivity, response.Id);
```

### <a name="using-nodejs"></a>Utilisation de Node.js

```javascript
var address =
{
    channelId: 'msteams',
    user: { id: userId },
    channelData: {
        tenant: {
            id: tenantId
        }
    },
    bot:
    {
        id: appId,
        name: appName
    },
    serviceUrl: session.message.address.serviceUrl,
    useAuth: true
}

var msg = new builder.Message().address(address);
msg.text('Hello, this is a notification');
bot.send(msg);
```

## <a name="creating-a-channel-conversation"></a>Créer une conversation de canal

Le bot de votre équipe peut créer une chaîne de réponse dans un canal. Si vous utilisez le Kit de développement logiciel (SDK) Node.js Teams, utilisez `startReplyChain()`, qui vous donne une adresse complète avec l’ID d’activité et l’ID de conversation corrects. Si vous utilisez C#, consultez l’exemple ci-dessous.

Vous pouvez également utiliser l’API REST et émettre une requête POST pour [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ressource.

### <a name="net-example-from-this-sample"></a>Exemple .NET (à partir de [cet exemple](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))

```csharp
using Microsoft.Bot.Builder.Dialogs;
using Microsoft.Bot.Connector;
using Microsoft.Bot.Connector.Teams.Models;
using Microsoft.Teams.TemplateBotCSharp.Properties;
using System;
using System.Threading.Tasks;

namespace Microsoft.Teams.TemplateBotCSharp.Dialogs
{
    [Serializable]
    public class ProactiveMsgTo1to1Dialog : IDialog<object>
    {
        public async Task StartAsync(IDialogContext context)
        {
            if (context == null)
            {
                throw new ArgumentNullException(nameof(context));
            }

            var channelData = context.Activity.GetChannelData<TeamsChannelData>();
            var message = Activity.CreateMessageActivity();
            message.Text = "Hello World";

            var conversationParameters = new ConversationParameters
            {
                  IsGroup = true,
                  ChannelData = new TeamsChannelData
                  {
                      Channel = new ChannelInfo(channelData.Channel.Id),
                  },
                  Activity = (Activity) message
            };

            MicrosoftAppCredentials.TrustServiceUrl(serviceUrl, DateTime.MaxValue);
            var connectorClient = new ConnectorClient(new Uri(activity.ServiceUrl));
            var response = await connectorClient.Conversations.CreateConversationAsync(conversationParameters);

            context.Done<object>(null);
        }
    }
}
```

## <a name="see-also"></a>Voir aussi

[Exemples Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
