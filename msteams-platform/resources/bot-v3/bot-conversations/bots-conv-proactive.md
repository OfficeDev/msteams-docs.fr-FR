---
title: Messages proactifs
description: Décrit bots peuvent commencer une conversation dans Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: équipes scénarios proactives messagerie conversation bot
ms.openlocfilehash: baf148d0f4d0a669de582dfca70ed5d5bed0274c
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566788"
---
# <a name="proactive-messaging-for-bots"></a>Messagerie proactive pour les bots

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Un message proactif est un message qui est envoyé par un bot pour démarrer une conversation. Vous voudrez peut-être que votre bot démarre une conversation pour diverses raisons, notamment :

* Messages de bienvenue pour les conversations personnelles bot.
* Réponses au sondage.
* Notifications d’événements externes.

Envoyer un message pour démarrer un nouveau thread de conversation est différent de l’envoi d’un message en réponse à une conversation existante : lorsque votre bot commence une nouvelle conversation, il n’y a pas de conversation préexistant pour poster le message. Afin d’envoyer un message proactif, vous devez :

1. [Décidez ce que vous allez dire](#best-practices-for-proactive-messaging)
1. [Obtenez l’id unique de l’utilisateur et l’id du locataire](#obtain-necessary-user-information)
1. [Envoyer le message](#examples)

Lors de la  création de messages `MicrosoftAppCredentials.TrustServiceUrl` proactifs, vous devez appeler et passer dans l’URL du service avant de `ConnectorClient` créer le que vous utiliserez pour envoyer le message. Si vous ne le faites pas, votre application recevra une `401: Unauthorized` réponse. Pour plus d’informations, voir [les échantillons ci-dessous](#net-example-from-this-sample).

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques pour la messagerie proactive

L’envoi de messages proactifs aux utilisateurs peut être un moyen très efficace de communiquer avec vos utilisateurs. Toutefois, de leur point de vue, ce message peut sembler leur venir complètement sans lempt, et dans le cas des messages de bienvenue sera la première fois qu’ils ont interagi avec votre application. En tant que tel, il est très important d’utiliser cette fonctionnalité avec parcimonie (ne pas spam vos utilisateurs), et de leur fournir suffisamment d’informations pour leur faire comprendre pourquoi ils sont messages.

Les messages proactifs sont généralement classés en deux catégories : les messages de bienvenue ou les messages de notification.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lorsque vous utilisez la messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que pour la plupart des personnes recevant le message, ils n’auront aucun contexte pour expliquer pourquoi ils le reçoivent. C’est aussi la première fois qu’ils interagissent avec votre application; c’est l’occasion de créer une bonne première impression. Les meilleurs messages de bienvenue seront les suivants :

* **Pourquoi reçoivent-ils ce message?** Il devrait être très clair pour l’utilisateur pourquoi ils reçoivent le message. Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et potentiellement qui l’a installé.
* **Qu’est-ce que tu offres?** Que peuvent-ils faire avec votre application ? Quelle valeur pouvez-vous leur apporter?
* **Que devraient-ils faire ensuite?** Invitez-les à essayer une commande ou à interagir d’une manière ou d’une autre avec votre application.

### <a name="notification-messages"></a>Les messages de notification

Lorsque vous utilisez la messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs ont un chemin clair pour prendre des mesures communes basées sur votre notification, et une compréhension claire des raisons pour lesquelles la notification s’est produite. Les bons messages de notification incluent généralement :

* **Que s'est-il passé?.** Une indication claire de ce qui s’est passé pour causer la notification.
* **Ce qu’il est arrivé à.** Il devrait être clair quel élément / chose a été mis à jour pour causer la notification.
* **Qui l’ai fait.** Qui pris les mesures qui ont causé l’envoi de la notification.
* **Ce qu’ils peuvent faire.** Facilitez la prise de mesures par vos utilisateurs en fonction de vos notifications.
* **Comment ils peuvent se retirer.** Vous devez fournir un chemin pour que les utilisateurs se retirent des notifications supplémentaires.

## <a name="obtain-necessary-user-information"></a>Obtenir les informations nécessaires sur les utilisateurs

Bots peut créer de nouvelles conversations avec un utilisateur Microsoft Teams en obtenant l’identifiant unique de *l’utilisateur et l’iD* du *locataire.* Vous pouvez obtenir ces valeurs en utilisant l’une des méthodes suivantes :

* En [récupérant la liste d’équipe à](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) partir d’un canal dans qui votre application est installée.
* En les tafonant lorsqu’un [utilisateur interagit avec votre bot dans un canal.](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)
* Lorsqu’un @mentioned [dans une conversation de](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions) canal, le bot fait partie de.
* En les caching lorsque vous [recevez l’événement `conversationUpdate` ](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) lorsque votre application est installée dans une portée personnelle, ou de nouveaux membres sont ajoutés à un canal ou un chat de groupe qui.

### <a name="proactively-install-your-app-using-graph"></a>Installez proactivement votre application à l’aide Graph

> [!Note]
> L’installation proactive d’applications à l’aide d’un graphique est actuellement en version bêta.

Parfois, il peut être nécessaire de transmettre des messages proactifs aux utilisateurs qui n’ont pas installé ou interagi avec votre application auparavant. Par exemple, vous souhaitez utiliser le communicateur de [l’entreprise pour envoyer](~/samples/app-templates.md#company-communicator) des messages à l’ensemble de votre organisation. Pour ce scénario, vous pouvez utiliser l’API Graph pour installer proactivement votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir de `conversationUpdate` l’événement que votre application recevra lors de l’installation.

Vous ne pouvez installer que des applications qui se trouvent dans votre catalogue d’applications organisationnelles ou dans Teams’App Store.

Voir [Installer des applications pour les utilisateurs](/graph/teams-proactive-messaging) dans la documentation Graph pour plus de détails. Il ya aussi un [échantillon dans .NET](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176).

## <a name="examples"></a>Exemples

Assurez-vous que vous authentifiez et avez un jeton porteur avant de créer une nouvelle conversation à l’aide de l’API REST.

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

Vous devez fournir l’identifiant de l’utilisateur et l’identifiant du locataire. Si l’appel réussit, l’API revient avec l’objet de réponse suivant.

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

Cet ID est l’iD de conversation unique du chat personnel. Veuillez stocker cette valeur et la réutiliser pour les interactions futures avec l’utilisateur.

### <a name="using-net"></a>Utilisation de .NET

Cet exemple utilise le [paquet Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet.

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

Le bot de votre équipe peut créer une chaîne de réponse dans un canal. Si vous utilisez le SDK Node.js Teams, utilisez-le qui `startReplyChain()` vous donne une adresse entièrement remplie avec l’id d’activité correct et l’id de conversation. Si vous utilisez C#, voir l’exemple ci-dessous.

Vous pouvez également utiliser l’API REST et émettre une demande POST de [`/conversations`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?#start-a-conversation) ressources.

### <a name="net-example-from-this-sample"></a>Exemple .NET (à partir [de cet échantillon)](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/32c39268d60078ef54f21fb3c6f42d122b97da22/template-bot-master-csharp/src/dialogs/examples/teams/ProactiveMsgTo1to1Dialog.cs)

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

[Échantillons de Bot Framework](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)