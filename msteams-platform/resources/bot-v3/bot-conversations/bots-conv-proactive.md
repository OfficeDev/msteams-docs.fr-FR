---
title: Messagerie proactive pour les bots
description: Découvrez comment utiliser la messagerie proactive pour les bots dans Microsoft Teams
ms.topic: conceptual
ms.localizationpriority: medium
keywords: scénarios d’équipes bot de conversation de messagerie proactive
ms.openlocfilehash: 9b554699a86c369da92d9fc7512a098dc8b5a7bf
ms.sourcegitcommit: 3dc9b539c6f7fbfb844c47a78e3b4d2200dabdad
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/31/2022
ms.locfileid: "64571004"
---
# <a name="proactive-messaging-for-bots"></a>Messagerie proactive pour les bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un message proactif est un message envoyé par un bot pour démarrer une conversation. Vous voudrez peut-être que votre bot démarre une conversation pour diverses raisons, notamment :

* L’envoi de messages de bienvenue pour les conversations personnelles par bot
* Les réponses aux sondages
* Les notifications d’événements externes

L’envoi d’un message pour démarrer un nouveau thread de conversation est différent de l’envoi d’un message en réponse à une conversation existante : lorsque votre bot démarre une nouvelle conversation, il n’y a pas de conversation pré-existante pour publier le message. Pour envoyer un message proactif, vous devez :

1. [Décider de ce que vous allez dire](#best-practices-for-proactive-messaging)
1. [Obtenir l’ID unique et l’ID client de l’utilisateur](#obtain-necessary-user-information)
1. [Envoyer le message](#examples)

Lorsque vous créez des  messages proactifs`MicrosoftAppCredentials.TrustServiceUrl`, vous devez appeler et transmettre l’URL `ConnectorClient` du service avant de créer l’url utilisée pour envoyer le message. Si ce n’est pas le cas, votre `401: Unauthorized` application reçoit une réponse. Pour plus d’informations, [voir les exemples ci-dessous](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques en matière de messagerie proactive

L’envoi de messages proactifs est un moyen efficace de communiquer avec vos utilisateurs. Toutefois, du point de vue des utilisateurs, le message s’affiche de manière spontanée. Lorsqu’il y a un message de bienvenue, il s’agira de leur première interaction avec votre application. Il est important d’utiliser cette fonctionnalité et de fournir des informations complètes à l’utilisateur pour comprendre l’objectif de ce message.

Les messages proactifs sont généralement classés en deux catégories : les messages de bienvenue ou les messages de notification.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lorsque vous utilisez une messagerie proactive pour envoyer un message de bienvenue à un utilisateur, assurez-vous que, du point de vue de l’utilisateur, le message s’affiche de manière non improvisée. Lorsqu’il y a un message de bienvenue, il s’agira de leur première interaction avec votre application. Les meilleurs messages de bienvenue sont les suivants :

* **Pourquoi ils reçoivent ce message** : l’utilisateur doit savoir clairement pourquoi il reçoit ce message. Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et éventuellement qui l’a installé.
* **Que proposez-vous** : que peuvent-ils faire avec votre application ? Quelle valeur pouvez-vous leur apporter ?
* **Que doivent-ils faire ensuite** : invitez-les à essayer une commande ou interagissez avec votre application d’une certaine façon.

### <a name="notification-messages"></a>Les messages de notification

Lorsque vous utilisez une messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs ont un chemin d’accès clair pour effectuer des actions courantes en fonction de votre notification et comprendre clairement pourquoi la notification s’est produite. Les messages de notification de bonne qualité incluent généralement :

* **Ce qui s’est** passé : une indication claire de ce qui est arrivé à l’origine de la notification.
* **Ce qu’il s’est passé** : il doit être clair quel élément/élément a été mis à jour pour provoquer la notification.
* **Qui l’avez-Qui** : Qui l’action à l’origine de l’envoi de la notification ?
* **Ce qu’ils peuvent faire à ce sujet** : faciliter la tâche des utilisateurs en fonction de vos notifications.
* **Comment ils peuvent refuser :** fournissez un chemin d’accès aux utilisateurs pour qu’ils ne choisissent pas d’autres notifications.

## <a name="obtain-necessary-user-information"></a>Obtenir les informations utilisateur nécessaires

Les bots peuvent créer des conversations avec un utilisateur Microsoft Teams en obtenant son *ID unique* et son *ID client.* Vous pouvez obtenir ces valeurs à l’aide de l’une des méthodes suivantes :

* En [extraire la liste de l’équipe](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) à partir d’un canal où votre application est installée.
* En les mettre en cache lorsqu’un utilisateur [interagit avec votre bot dans un canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).
* Lorsqu’un utilisateur est [@mentioned dans une conversation de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) , le bot fait partie de.
* En les mettre [`conversationUpdate`](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) en cache lorsque vous recevez l’événement lorsque votre application est installée dans une étendue personnelle, ou que de nouveaux membres sont ajoutés à une conversation de canal ou de groupe qui.

### <a name="proactively-install-your-app-using-graph"></a>Installer votre application de manière proactive en utilisant Graph

> [!Note]
> L’installation proactive d’applications à l’aide d’un graphique est actuellement en version bêta.

Parfois, il peut s’agir de messages de manière proactive pour les utilisateurs qui n’ont pas installé votre application ou qui n’ont pas interagi avec celle-ci précédemment. Par exemple, vous souhaitez utiliser le [communicateur d’entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’échelle de votre organisation. Pour ce scénario, vous pouvez utiliser le API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache `conversationUpdate` les valeurs nécessaires à partir de l’événement que votre application recevra lors de l’installation.

Vous pouvez uniquement installer des applications qui se trouver dans votre catalogue d’applications d’organisation ou dans Teams’application store.

Pour [plus d’informations](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true), voir Installer des applications pour les utilisateurs Graph documentation. Il existe également un [exemple dans .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Exemples

Veillez à vous authentifier et à avoir un jeton de support avant de créer une conversation à l’aide de l’API REST.

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

Vous devez fournir l’identifiant utilisateur et l’identifiant du client. Si l’appel réussit, l’API renvoie avec l’objet de réponse suivant.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Cet ID est l’ID de conversation unique de la conversation personnelle. Stockez cette valeur et réutilisez-la pour les interactions futures avec l’utilisateur.

### <a name="using-net"></a>Utilisation de .NET

Cet exemple utilise [le package Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.

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

Le bot de votre équipe peut créer une chaîne de réponse dans un canal. Si vous utilisez le SDK Node.js Teams, `startReplyChain()`utilisez , qui vous donne une adresse entièrement remplie avec l’ID d’activité et l’ID de conversation corrects. Si vous utilisez C#, consultez l’exemple ci-dessous.

Vous pouvez également utiliser l’API REST et émettre une demande POST à la [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ressource.

### <a name="net-example-from-this-sample"></a>Exemple .NET (à partir [de cet exemple](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))

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
