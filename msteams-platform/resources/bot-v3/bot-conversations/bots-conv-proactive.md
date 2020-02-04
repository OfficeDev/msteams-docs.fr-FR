---
title: Messages proactifs
description: Décrit les robots pouvant démarrer une conversation dans Microsoft teams
keywords: scénarios de teams robot de conversation de messagerie proactive
ms.openlocfilehash: c5c779b7ec5733b19366ae73053ef7d45ca6c1d6
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673590"
---
# <a name="proactive-messaging-for-bots"></a>Messagerie proactive pour les robots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un message proactif est un message qui est envoyé par un bot pour démarrer une conversation. Vous souhaiterez peut-être que votre bot entame une conversation pour plusieurs raisons, notamment :

* Messages de bienvenue pour les conversations personnelles de robots
* Interrogation des réponses
* Notifications d’événements externes

L’envoi d’un message pour démarrer un nouveau thème de conversation est différent de celui de l’envoi d’un message en réponse à une conversation existante : lorsque votre bot démarre une nouvelle conversation, il n’existe pas de conversation préexistante vers laquelle publier le message. Pour envoyer un message proactif, vous devez :

1. [Décider de ce que vous allez dire](#best-practices-for-proactive-messaging)
1. [Obtenir l’ID unique et l’ID de client uniques de l’utilisateur](#obtain-necessary-user-information)
1. [Envoyer le message](#examples)

Lors de la création de messages proactifs que vous **devez** appeler `MicrosoftAppCredentials.TrustServiceUrl`, et transmettre l' `ConnectorClient` URL du service avant de créer le message que vous allez utiliser pour envoyer le message. Si vous ne le faites pas, votre application recevra une `401: Unauthorized` réponse. Consultez [les exemples ci-dessous](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques pour la messagerie proactive

L’envoi de messages proactifs aux utilisateurs peut être un moyen très efficace de communiquer avec vos utilisateurs. Toutefois, à partir de leur perspective, ce message peut sembler indésirable et, dans le cas de messages de bienvenue, il s’agit de la première fois qu’ils interagissent avec votre application. Par conséquent, il est très important d’utiliser cette fonctionnalité avec parcimonie (ne pas envoyer de courrier indésirable) et de leur fournir suffisamment d’informations pour les informer de la raison pour laquelle ils reçoivent des messages.

Les messages proactifs font généralement partie de l’une des deux catégories suivantes : messages d’accueil ou notifications.

### <a name="welcome-messages"></a>Messages de bienvenue

Lors de l’utilisation de la messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que pour la plupart des personnes qui reçoivent le message, il n’y aura pas de contexte pour la raison pour laquelle ils le reçoivent. Il s’agit également de la première fois qu’ils interagissent avec votre application ; Il s’agit de votre opportunité de créer une bonne première impression. Les meilleurs messages d’accueil sont les suivants :

* **Pourquoi reçoit-il ce message ?** Il doit être très clair que les utilisateurs reçoivent le message. Si votre robot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, indiquez-lui quel canal il a été installé et éventuellement qui l’a installé.
* **Ce que vous proposez.** Qu’est-il possible de faire avec votre application ? Quelle valeur pouvez-vous leur apporter ?
* **Que dois-je faire ensuite ?** Invitez-les à essayer une commande ou à interagir avec votre application d’une certaine façon.

### <a name="notification-messages"></a>Messages de notification

Lors de l’utilisation de la messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs disposent d’un chemin d’accès clair afin de prendre des mesures courantes en fonction de votre notification et de bien comprendre la raison pour laquelle la notification s’est produite. Les messages de notification valides sont généralement les suivants :

* **Que s'est-il passé.** Indication claire de l’origine de la notification.
* **Ce qu’il y a eu.** Il doit être clair quel élément/élément a été mis à jour pour déclencher la notification.
* **Qui a fait ça.** Qui a effectué l’action qui a provoqué l’envoi de la notification.
* **Ce qu’ils peuvent faire.** Permettre aux utilisateurs de prendre facilement des mesures en fonction de vos notifications.
* **Comment les désactiver.** Vous devez fournir un chemin d’accès permettant aux utilisateurs de désactiver les notifications supplémentaires.

## <a name="obtain-necessary-user-information"></a>Obtenir les informations utilisateur nécessaires

Les robots peuvent créer de nouvelles conversations avec un utilisateur individuel de Microsoft teams en obtenant l’ID *unique* et l' *ID de client* de l’utilisateur. Vous pouvez obtenir ces valeurs à l’aide de l’une des méthodes suivantes :

* En [extrayant la liste de l’équipe](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) à partir d’un canal dans lequel votre application est installée.
* En les mettant en cache lorsqu’un utilisateur [interagit avec votre robot dans un canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md).
* Lorsqu’un utilisateur est [@mentioned dans une conversation de canal](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) dont le robot fait partie.
* En les mettant en cache lorsque vous [recevez l' `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) événement lorsque votre application est installée dans une étendue personnelle, ou que de nouveaux membres sont ajoutés à un canal ou à une conversation de groupe qui

### <a name="proactively-install-your-app-using-graph"></a>Installer de manière proactive votre application à l’aide de Graph

> [!Note]
> L’installation proactive d’applications à l’aide de Graph est actuellement en version bêta.

Parfois, il peut s’avérer nécessaire de messageer de manière proactive les utilisateurs qui n’ont pas installé ou interagi avec votre application précédemment. Par exemple, vous souhaitez utiliser l' [entreprise Communicator](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation. Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs `conversationUpdate` nécessaires à partir de l’événement que votre application recevra lors de l’installation.

Vous ne pouvez installer que les applications figurant dans le catalogue d’applications de votre organisation ou dans le magasin d’applications Teams.

Pour plus d’informations, consultez la rubrique [installer des applications pour les utilisateurs](/graph/teams-proactive-messaging) dans la documentation Graph. Il existe également un [exemple dans .net](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Exemples

Assurez-vous d’authentifier et de posséder un jeton de support avant de créer une conversation à l’aide de l’API REST.

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

Cet ID est l’ID de conversation unique de la conversation personnelle. Veuillez stocker cette valeur et la réutiliser pour les futures interactions avec l’utilisateur.

### <a name="using-net"></a>Utilisation de .NET

Cet exemple utilise le package NuGet [Microsoft. Bot. Connector. teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) .

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

### <a name="using-nodejs"></a>Utilisation de node. js

Cet exemple utilise le package NPM [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) .

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

## <a name="creating-a-channel-conversation"></a>Création d’une conversation de canal

Votre robot ajouté en équipe peut effectuer des publications dans un canal pour créer une chaîne de réponse. Si vous utilisez le kit de développement logiciel (SDK) node `startReplyChain()` . js Teams, utilisez qui vous fournit une adresse complète avec l’ID d’activité et l’ID de conversation corrects. Si vous utilisez C#, consultez l’exemple ci-dessous.

Vous pouvez également utiliser l’API REST et émettre une requête POST à [`/conversations`](https://docs.microsoft.com/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) la ressource.

### <a name="net-example-from-this-samplehttpsgithubcomofficedevmicrosoft-teams-sample-complete-csharpblob32c39268d60078ef54f21fb3c6f42d122b97da22template-bot-master-csharpsrcdialogsexamplesteamsproactivemsgto1to1dialogcs"></a>Exemple .NET (de [cet exemple](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs))

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
