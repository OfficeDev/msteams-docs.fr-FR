---
title: Messages proactifs
description: Décrit les bots qui peuvent démarrer une conversation dans Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: scénarios teams de bot de conversation de messagerie proactive
ms.openlocfilehash: 82282c4e2a2d48acad8f4bb384976906296be8f9
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630466"
---
# <a name="proactive-messaging-for-bots"></a>Messagerie proactive pour les bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un message proactif est un message envoyé par un bot pour démarrer une conversation. Vous voudrez peut-être que votre bot démarre une conversation pour diverses raisons, notamment :

* Messages de bienvenue pour les conversations de bot personnels.
* Réponses aux sondages.
* Notifications d’événements externes.

L’envoi d’un message pour démarrer un nouveau thread de conversation est différent de l’envoi d’un message en réponse à une conversation existante : lorsque votre bot démarre une nouvelle conversation, il n’y a aucune conversation pré-existante vers qui publier le message. Pour envoyer un message proactif, vous devez :

1. [Décider de ce que vous allez dire](#best-practices-for-proactive-messaging)
1. [Obtenir l’ID unique et l’ID client de l’utilisateur](#obtain-necessary-user-information)
1. [Envoyer le message](#examples)

Lorsque vous créez des messages proactifs, vous devez appeler et transmettre l’URL du service avant de créer le message que vous utiliserez pour envoyer le  `MicrosoftAppCredentials.TrustServiceUrl` `ConnectorClient` message. Si ce n’est pas le cas, votre application reçoit une `401: Unauthorized` réponse. Pour plus d’informations, [voir les exemples ci-dessous.](#net-example-from-this-sample)

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques en matière de messagerie proactive

L’envoi de messages proactifs aux utilisateurs peut être un moyen très efficace de communiquer avec vos utilisateurs. Toutefois, de leur point de vue, ce message peut leur sembler totalement non improvisé et, dans le cas des messages de bienvenue, il s’agit de la première fois qu’ils interagissent avec votre application. En tant que tel, il est très important d’utiliser cette fonctionnalité avec parcimonie (ne pas envoyer de courrier indésirable à vos utilisateurs) et de leur fournir suffisamment d’informations pour leur faire comprendre pourquoi ils sont envoyés.

Les messages proactifs sont généralement classés en deux catégories : les messages de bienvenue ou les messages de notification.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lorsque vous utilisez une messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que pour la plupart des personnes qui reçoivent le message, elles n’ont aucun contexte pour la raison pour laquelle elles le reçoivent. C’est également la première fois qu’ils interagissent avec votre application . c’est l’occasion de créer une bonne première impression. Les meilleurs messages de bienvenue sont les suivants :

* **Pourquoi reçoivent-ils ce message ?** Il doit être très clair pour l’utilisateur pourquoi il reçoit le message. Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et éventuellement qui l’a installé.
* **Que proposez-vous ?** Que peuvent-ils faire avec votre application ? Quelle valeur pouvez-vous leur apporter ?
* **Que doivent-ils faire ensuite ?** Invitez-les à essayer une commande ou à interagir avec votre application d’une certaine façon.

### <a name="notification-messages"></a>Les messages de notification

Lorsque vous utilisez une messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs ont un chemin d’accès clair pour effectuer des actions courantes en fonction de votre notification et comprendre clairement pourquoi la notification s’est produite. Les messages de notification de bonne qualité incluent généralement :

* **Que s'est-il passé.** Indication claire de la cause de la notification.
* **Qu’est-ce qu’il s’est passé ?** Il doit être clair quel élément/élément a été mis à jour pour provoquer la notification.
* **Qui l’a fait.** Qui l’action à l’origine de l’envoi de la notification.
* **Ce qu’ils peuvent faire à ce sujet.** Faites en sorte que vos utilisateurs prennent facilement des mesures en fonction de vos notifications.
* **Comment ils peuvent refuser.** Vous devez fournir un chemin d’accès aux utilisateurs pour qu’ils ne choisissent pas d’autres notifications.

## <a name="obtain-necessary-user-information"></a>Obtenir les informations utilisateur nécessaires

Les bots peuvent créer des conversations avec un utilisateur Microsoft Teams en obtenant *l’ID unique* et l’ID *client de l’utilisateur.* Vous pouvez obtenir ces valeurs à l’aide de l’une des méthodes suivantes :

* En [extraire la liste de l’équipe](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) à partir d’un canal où votre application est installée.
* En les mettre en cache lorsqu’un utilisateur [interagit avec votre bot dans un canal.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)
* Lorsqu’un utilisateur est @mentioned dans une conversation de [canal,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) le bot fait partie de.
* En les mettre [ `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) en cache lorsque vous recevez l’événement lorsque votre application est installée dans une étendue personnelle, ou que de nouveaux membres sont ajoutés à une conversation de canal ou de groupe qui.

### <a name="proactively-install-your-app-using-graph"></a>Installer votre application de manière proactive à l’aide Graph

> [!Note]
> L’installation proactive d’applications à l’aide d’un graphique est actuellement en version bêta.

Parfois, il peut être nécessaire de transmettre un message de manière proactive aux utilisateurs qui n’ont pas installé votre application ou n’ont pas interagi avec celle-ci précédemment. Par exemple, vous souhaitez utiliser le communicateur [d’entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation. Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir de l’événement que votre application recevra lors de `conversationUpdate` l’installation.

Vous pouvez uniquement installer des applications qui se trouver dans votre catalogue d’applications d’organisation ou dans Teams’application store.

Pour plus [d’informations,](/graph/api/userteamwork-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true) voir Installer des applications pour les utilisateurs Graph documentation. Il existe également un [exemple dans .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

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

Vous devez fournir l’ID d’utilisateur et l’ID de client. Si l’appel réussit, l’API renvoie avec l’objet de réponse suivant.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Cet ID est l’ID de conversation unique de la conversation personnelle. Stockez cette valeur et réutilisez-la pour les interactions futures avec l’utilisateur.

### <a name="using-net"></a>Utilisation de .NET

Cet exemple utilise le package [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.

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

Le bot de votre équipe peut créer une chaîne de réponse dans un canal. Si vous utilisez le SDK Node.js Teams, utilisez une adresse complète avec l’ID d’activité et `startReplyChain()` l’ID de conversation corrects. Si vous utilisez C#, consultez l’exemple ci-dessous.

Vous pouvez également utiliser l’API REST et émettre une demande POST à la [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ressource.

### <a name="net-example-from-this-sample"></a>Exemple .NET (à partir [de cet exemple)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)

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
