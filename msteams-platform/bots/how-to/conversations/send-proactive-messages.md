---
title: Envoi de messages proactifs
author: clearab
description: Comment envoyer des messages proactifs avec votre robot Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2dfb8e18243079ca38d505f4b80deb7abf2de32f
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874848"
---
# <a name="send-proactive-messages"></a>Envoi de messages proactifs

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un message proactif est un message envoyé par un bot qui n’est pas en réponse directe à une demande d’un utilisateur. Cela peut inclure des messages comme :

* Les messages de bienvenue
* Notifications
* Messages planifiés

Pour que votre bot puisse envoyer un message proactif, il doit avoir accès à l’utilisateur, à la conversation de groupe ou à l’équipe à laquelle vous souhaitez envoyer le message. Pour une conversation de groupe ou une équipe, cela signifie que l’application qui contient votre robot doit d’abord être installée à cet emplacement. Vous pouvez [installer votre application de façon proactive en utilisant Graph](#proactively-install-your-app-using-graph) dans une équipe, si nécessaire, ou utiliser une [stratégie d’application](/microsoftteams/teams-custom-app-policies-and-settings) pour envoyer des applications à des équipes et des utilisateurs de votre client. Pour les utilisateurs, votre application doit être installée pour cet utilisateur ou votre utilisateur doit faire partie d’une équipe où votre application est installée.

L’envoi d’un message proactif est différent de l’envoi d’un message standard dans lequel vous n’aurez pas `turnContext` à utiliser une réponse pour répondre. Vous devrez peut-être également créer la conversation (par exemple, une nouvelle conversation un-à-un ou un nouveau fil de conversation dans un canal) avant d’envoyer le message. Vous ne pouvez pas créer une nouvelle conversation de groupe ou une nouvelle chaîne dans une équipe avec la messagerie proactive.

À un niveau élevé, les étapes que vous devez effectuer pour envoyer un message proactif sont les suivantes :

1. [Obtenir l’ID d’utilisateur ou l’ID d’équipe/de canal](#get-the-user-id-or-teamchannel-id) (le cas échéant).
1. [Créez le thème conversation ou conversation](#create-the-conversation) (le cas échéant).
1. [Obtenir l’ID de conversation](#get-the-conversation-id).
1. [Envoyer le message](#send-the-message).

Les extraits de code dans la section [exemples](#examples) ci-dessous permettent de créer une conversation un-à-un, consultez la section [références](#references) pour obtenir des liens vers des exemples de travail complets pour les conversations et les groupes/canaux un-à-un.

## <a name="get-the-user-id-or-teamchannel-id"></a>Obtenir l’ID d’utilisateur ou l’ID d’équipe/de canal

Si vous devez créer un nouveau thème de conversation ou de conversation dans un canal, vous aurez d’abord besoin de l’ID approprié pour créer la conversation. Vous pouvez recevoir/récupérer cet ID de plusieurs façons :

1. Lorsque votre application est installée dans un contexte particulier, vous recevez une [ `onMembersAdded` activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Lorsqu’un nouvel utilisateur est ajouté à un contexte dans lequel votre application est installée, vous recevez une [ `onMembersAdded` activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Vous pouvez récupérer la [liste des canaux](~/bots/how-to/get-teams-context.md) d’une équipe installée sur votre application.
1. Vous pouvez récupérer la [liste des membres](~/bots/how-to/get-teams-context.md) d’une équipe installée sur votre application.
1. Chaque activité reçue par votre robot contient les informations nécessaires.

Quelle que soit la façon dont vous obtenez les informations, vous devez stocker le `tenantId` et le `userId` ou `channelId` pour créer une conversation. Vous pouvez également utiliser le `teamId` pour créer un fil de conversation dans le canal général/par défaut d’une équipe.

Le `userId` est unique pour votre ID de robot et un utilisateur particulier, vous ne pouvez pas les réutiliser entre les robots. Le `channelId` est global, toutefois, votre robot _doit_ être installé dans l’équipe avant de pouvoir envoyer un message proactif à un canal.

## <a name="create-the-conversation"></a>Créer la conversation

Une fois que vous avez les informations de l’utilisateur/du canal, vous devez créer la conversation si elle n’existe pas déjà (ou si vous ne connaissez pas le `conversationId` ). Vous devez uniquement créer la conversation une seule fois ; Veillez à stocker la `conversationId` valeur ou l' `conversationReference` objet à utiliser à l’avenir.

## <a name="get-the-conversation-id"></a>Obtenir l’ID de conversation

Une fois la conversation créée, vous devez utiliser l' `conversationReference` objet ou le `conversationId` et le `tenantId` pour envoyer le message. Vous pouvez obtenir cet ID en créant la conversation ou en la stockant à partir de n’importe quelle activité qui vous a été envoyée à partir de ce contexte. Assurez-vous que vous stockez cet ID.

## <a name="send-the-message"></a>Envoyer le message

Maintenant que vous disposez des informations d’adresse appropriées, vous pouvez envoyer votre message. Si vous utilisez le kit de développement logiciel (SDK), vous pouvez le faire à l’aide de la `continueConversation` méthode et du `conversationId` et `tenantId` pour effectuer un appel d’API direct.  Vous devrez définir `conversationParameters` correctement l’envoi de votre message : consultez les [exemples](#examples) ci-dessous ou utilisez l’un des exemples figurant dans la section [références](#references) .

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques pour la messagerie proactive

L’envoi de messages proactifs aux utilisateurs peut être un moyen très efficace de communiquer avec vos utilisateurs. Toutefois, à partir de leur perspective, ce message peut sembler totalement indésirable et, dans le cas de messages de bienvenue, il sera la première fois qu’il interagit avec votre application. Par conséquent, il est très important d’utiliser cette fonctionnalité avec parcimonie (ne pas envoyer de courrier indésirable) et de fournir suffisamment d’informations pour permettre aux utilisateurs de comprendre la raison pour laquelle ils reçoivent des messages.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lors de l’utilisation de la messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que, pour la plupart des personnes qui reçoivent le message, il n’y aura pas de contexte pour les raisons pour lesquelles ils le reçoivent. Il s’agit également de la première fois qu’ils interagissent avec votre application ; Il s’agit de votre opportunité de créer une bonne première impression. Les meilleurs messages d’accueil sont les suivants :

* **Raisons pour lesquelles un utilisateur reçoit le message.** Il doit être très clair que les utilisateurs reçoivent le message. Si votre robot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, indiquez-lui quel canal il a été installé et éventuellement qui l’a installé.
* **Ce que vous proposez.** Qu’est-il possible de faire avec votre application ? Quelle valeur pouvez-vous leur apporter ?
* **Que dois-je faire ensuite ?** Invitez-les à essayer une commande ou à interagir avec votre application d’une certaine façon.

N’oubliez pas que les messages de bienvenue médiocres peuvent amener les utilisateurs à bloquer votre robot. Vous devez consacrer suffisamment de temps à la conception de vos messages de bienvenue et les parcourir s’ils n’ont pas l’effet escompté.

### <a name="notification-messages"></a>Les messages de notification

Lors de l’utilisation de la messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs disposent d’un chemin d’accès clair afin de prendre des mesures courantes en fonction de votre notification et de bien comprendre la raison pour laquelle la notification s’est produite. Les messages de notification valides sont généralement les suivants :

* **Que s'est-il passé.** Indication claire de l’origine de la notification.
* **Quel a été le résultat.** Il doit être clair quel élément/élément a été mis à jour pour déclencher la notification.
* **OMS/ce qui a été déclenché.** Les personnes ou les actions qui ont entraîné l’envoi de la notification.
* **Ce que les utilisateurs peuvent faire en réponse.** Permettre aux utilisateurs de prendre facilement des mesures en fonction de vos notifications.
* **Comment les utilisateurs peuvent-ils les désactiver** ? Vous devez fournir un chemin d’accès permettant aux utilisateurs de désactiver les notifications supplémentaires.

## <a name="proactively-install-your-app-using-graph"></a>Installer de manière proactive votre application à l’aide de Graph

> [!Note]
> L’installation proactive d’applications à l’aide de Microsoft Graph est actuellement en version bêta.

Parfois, il peut s’avérer nécessaire de messageer de manière proactive les utilisateurs qui n’ont pas installé ou interagi avec votre application précédemment. Par exemple, vous souhaitez utiliser l' [entreprise Communicator](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation. Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir de l’événement que votre application recevra lors de l' `conversationUpdate` installation.

Vous ne pouvez installer que les applications figurant dans le catalogue d’applications de votre organisation ou dans le magasin d’applications Teams.

Voir [installer des applications pour les utilisateurs](/graph/teams-proactive-messaging) dans la documentation Graph et l' [installation et la messagerie de robots proactifs dans teams avec Microsoft Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md). Il existe également un [exemple Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176)  sur la plateforme github.

## <a name="examples"></a>Exemples

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
private async Task MessageAllMembersAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var teamsChannelId = turnContext.Activity.TeamsGetChannelId();
    var serviceUrl = turnContext.Activity.ServiceUrl;
    var credentials = new MicrosoftAppCredentials(_appId, _appPassword);
    ConversationReference conversationReference = null;

    //Get the set of member IDs to send the message to
    var members = await GetPagedMembers(turnContext, cancellationToken);

    foreach (var teamMember in members)
    {
        var proactiveMessage = MessageFactory.Text($"Hello {teamMember.GivenName} {teamMember.Surname}. I'm a Teams conversation bot.");

        var conversationParameters = new ConversationParameters
        {
            IsGroup = false,
            Bot = turnContext.Activity.Recipient,
            Members = new ChannelAccount[] { teamMember },
            TenantId = turnContext.Activity.Conversation.TenantId,
        };
        //create the new one-to-one conversations
        await ((BotFrameworkAdapter)turnContext.Adapter).CreateConversationAsync(
            teamsChannelId,
            serviceUrl,
            credentials,
            conversationParameters,
            async (t1, c1) =>
            {
                //Get the conversationReference
                conversationReference = t1.Activity.GetConversationReference();
                //Send the proactive message
                await ((BotFrameworkAdapter)turnContext.Adapter).ContinueConversationAsync(
                    _appId,
                    conversationReference,
                    async (t2, c2) =>
                    {
                        await t2.SendActivityAsync(proactiveMessage, c2);
                    },
                    cancellationToken);
            },
            cancellationToken);
    }

    await turnContext.SendActivityAsync(MessageFactory.Text("All messages have been sent."), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```javascript

async messageAllMembersAsync(context) {
    const members = await this.getPagedMembers(context);

    members.forEach(async (teamMember) => {
        const message = MessageFactory.text('Hello ${ teamMember.givenName } ${ teamMember.surname }. I\'m a Teams conversation bot.');

        var ref = TurnContext.getConversationReference(context.activity);
        ref.user = teamMember;

        await context.adapter.createConversation(ref,
            async (t1) => {
                const ref2 = TurnContext.getConversationReference(t1.activity);
                await t1.adapter.continueConversation(ref2, async (t2) => {
                    await t2.sendActivity(message);
                });
            });
    });

    await context.sendActivity(MessageFactory.text('All messages have been sent.'));
}
```

# <a name="python"></a>[Python](#tab/python)

```python
async def _message_all_members(self, turn_context: TurnContext):
    team_members = await self._get_paged_members(turn_context)

    for member in team_members:
        conversation_reference = TurnContext.get_conversation_reference(
            turn_context.activity
        )

        conversation_parameters = ConversationParameters(
            is_group=False,
            bot=turn_context.activity.recipient,
            members=[member],
            tenant_id=turn_context.activity.conversation.tenant_id,
        )

        async def get_ref(tc1):
            conversation_reference_inner = TurnContext.get_conversation_reference(
                tc1.activity
            )
            return await tc1.adapter.continue_conversation(
                conversation_reference_inner, send_message, self._app_id
            )

        async def send_message(tc2: TurnContext):
            return await tc2.send_activity(
                f"Hello {member.name}. I'm a Teams conversation bot."
            )

        await turn_context.adapter.create_conversation(
            conversation_reference, get_ref, conversation_parameters
        )

    await turn_context.send_activity(
        MessageFactory.text("All messages have been sent")
    )

```

# <a name="json"></a>[JSON](#tab/json)

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

---

## <a name="references"></a>Références

Les exemples officiels de messagerie proactive sont répertoriés ci-dessous.

|  Non.  | Exemple de nom           | Description                                                                      | .NET    | JavaScript   | Python  |
|:--:|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|57|Concepts de base des conversations de teams  | Présente des notions de base des conversations dans Teams, y compris l’envoi de messages proactifs un-à-un.|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|58|Démarrer un nouveau thread dans un canal     | Illustre la création d’un nouveau thread dans un canal. |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

L’exemple ci-dessous illustre la quantité minimale d’informations nécessaires à l’envoi d’un message proactif (sans utiliser d' `conversationReference` objet). Cet exemple peut être utile si vous utilisez des appels d’API REST directement ou si vous n’avez pas stocké d' `conversationReference` objets complets.

* [Messagerie proactive teams](https://github.com/clearab/teamsProactiveMessaging)

## <a name="view-additional-code"></a>Afficher du code supplémentaire
>
> [!div class="nextstepaction"]
> [**Exemples de code de messagerie proactive teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>