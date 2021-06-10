---
title: Envoyer des messages proactifs
description: Décrit comment envoyer des messages proactifs avec Microsoft Teams bot.
ms.topic: conceptual
ms.author: anclear
localization_priority: Normal
Keywords: envoyer un message pour obtenir l’ID de conversation de l’ID de canal de l’ID de l’utilisateur
ms.openlocfilehash: ae651ac94b1b092374f6fae284b67070036b561f
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020918"
---
# <a name="send-proactive-messages"></a>Envoyer des messages proactifs

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un message proactif est un message envoyé par un bot qui ne répond pas à une demande d’un utilisateur. Cela peut inclure des messages, tels que :

* Les messages de bienvenue
* Notifications
* Messages programmés

Pour que votre bot envoie un message proactif à un utilisateur, une conversation de groupe ou une équipe, il doit avoir accès pour envoyer le message. Pour une conversation de groupe ou une équipe, l’application qui contient votre bot doit d’abord être installée à cet emplacement. Vous pouvez installer votre application de manière proactive à l’aide de [](/microsoftteams/teams-custom-app-policies-and-settings) [Microsoft Graph](#proactively-install-your-app-using-graph) dans une équipe, si nécessaire, ou utiliser une stratégie d’application pour faire sortir les applications vers les équipes et les utilisateurs de votre client. Pour les utilisateurs, votre application doit être installée pour l’utilisateur ou votre utilisateur doit faire partie d’une équipe sur laquelle votre application est installée.

L’envoi d’un message proactif est différent de l’envoi d’un message normal. Il n’est pas actif `turnContext` à utiliser pour une réponse. Vous devez créer la conversation avant d’envoyer le message. Par exemple, une nouvelle conversation un-à-un ou un nouveau thread de conversation dans un canal. Vous ne pouvez pas créer une conversation de groupe ou un nouveau canal dans une équipe avec une messagerie proactive.

**Pour envoyer un message proactif**

1. [Obtenez l’ID d’utilisateur, l’ID d’équipe ou l’ID](#get-the-user-id-team-id-or-channel-id)de canal, si nécessaire.
1. [Créez la conversation,](#create-the-conversation)si nécessaire.
1. [Obtenir l’ID de conversation](#get-the-conversation-id).
1. [Envoyer le message](#send-the-message).

Les extraits de code de la section [exemples](#samples) sont pour la création d’une conversation un-à-un. Pour obtenir des liens vers des exemples de travail complets pour les conversations un-à-un et les groupes ou canaux, voir [l’exemple de code.](#code-sample)

Pour utiliser efficacement les messages proactifs, consultez les meilleures pratiques en matière [de messagerie proactive.](#best-practices-for-proactive-messaging) Dans certains scénarios, vous devez installer votre application de manière proactive à [l’aide de Graph](#proactively-install-your-app-using-graph). Les extraits de code de la section [exemples](#samples) sont pour la création d’une conversation un-à-un. Pour obtenir des exemples de travail complets pour les conversations et les groupes ou canaux un-à-un, voir [l’exemple de code.](#code-sample)

## <a name="get-the-user-id-team-id-or-channel-id"></a>Obtenir l’ID d’utilisateur, l’ID d’équipe ou l’ID de canal

Pour créer une conversation ou un thread de conversation dans un canal, vous devez avoir l’ID correct. Vous pouvez recevoir ou récupérer cet ID à l’aide des informations suivantes :

* Lorsque votre application est installée dans un contexte particulier, vous recevez une [ `onMembersAdded` activité.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* Lorsqu’un nouvel utilisateur est ajouté à un contexte où votre application est installée, vous recevez une [ `onMembersAdded` activité.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* Vous pouvez récupérer la [liste des canaux dans](~/bots/how-to/get-teams-context.md) une équipe où votre application est installée.
* Vous pouvez récupérer la [liste des membres d’une](~/bots/how-to/get-teams-context.md) équipe sur laquelle votre application est installée.
* Chaque activité que reçoit votre bot doit contenir les informations requises.

Quelle que soit la façon dont vous obtenez les informations, vous devez stocker le ou pour `tenantId` `userId` créer une `channelId` conversation. Vous pouvez également l’utiliser pour créer un thread de conversation dans le canal général ou `teamId` par défaut d’une équipe.

Il `userId` est propre à votre ID de bot et à un utilisateur particulier. Vous ne pouvez pas réutiliser les `userId` bots. Il `channelId` s’agit d’une stratégie globale. Toutefois, votre bot doit être installé dans l’équipe avant de pouvoir envoyer un message proactif à un canal.

Une fois que vous avez les informations de l’utilisateur ou du canal, vous devez créer la conversation.

## <a name="create-the-conversation"></a>Créer la conversation

Vous devez créer la conversation si elle n’existe pas ou si vous ne connaissez pas le `conversationId` . Vous ne devez créer la conversation qu’une seule fois et stocker la `conversationId` valeur ou `conversationReference` l’objet.

Une fois la conversation créée, vous devez obtenir l’ID de conversation.

## <a name="get-the-conversation-id"></a>Obtenir l’ID de conversation

Utilisez `conversationReference` l’objet ou et pour envoyer le `conversationId` `tenantId` message. Vous pouvez obtenir cet ID en créant la conversation ou en la stockant à partir de n’importe quelle activité qui vous est envoyée à partir de ce contexte. Stockez cet ID pour référence.

Une fois que vous avez reçu les informations d’adresse appropriées, vous pouvez envoyer votre message.

## <a name="send-the-message"></a>Envoyer le message

Maintenant que vous avez les bonnes informations d’adresse, vous pouvez envoyer votre message. Si vous utilisez le SDK, vous devez utiliser la méthode et effectuer un appel `continueConversation` `conversationId` `tenantId` d’API direct. Vous devez définir correctement `conversationParameters` l’envoi de votre message. Consultez la section [exemples](#samples) ou utilisez l’un des exemples répertoriés dans la section [exemple de code.](#code-sample)

Si vous utilisez le SDK, vous devez utiliser la méthode et effectuer un appel `continueConversation` `conversationId` `tenantId` d’API direct pour envoyer le message. Vous devez définir correctement `conversationParameters` l’envoi de votre message.

Maintenant que vous avez envoyé le message proactif, vous devez suivre ces meilleures pratiques tout en envoyant des messages proactifs pour un meilleur échange d’informations entre les utilisateurs et le bot.

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques en matière de messagerie proactive

L’envoi de messages proactifs aux utilisateurs est un moyen très efficace de communiquer avec vos utilisateurs. Toutefois, de leur point de vue, ce message peut apparaître complètement non improvisé et, dans le cas des messages de bienvenue, c’est la première fois qu’ils interagissent avec votre application. Par conséquent, il est très important d’utiliser avec parcimonie la messagerie proactive, et non de mettre vos utilisateurs en courrier indésirable, et de fournir suffisamment d’informations pour que les utilisateurs comprennent pourquoi ils reçoivent les messages.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lorsque la messagerie proactive est utilisée pour envoyer un message de bienvenue à un utilisateur, il n’existe aucun contexte pour expliquer pourquoi les utilisateurs reçoivent le message. C’est également la première fois que les utilisateurs interagissent avec votre application. Il s’agit d’une opportunité de créer une bonne première impression. Les meilleurs messages de bienvenue doivent être les suivants :

* Pourquoi un utilisateur reçoit le message : il doit être très clair pour l’utilisateur pourquoi il reçoit le message. Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et qui l’a installé.
* Que proposez-vous : les utilisateurs doivent être en mesure d’identifier ce qu’ils peuvent faire avec votre application et la valeur que vous pouvez leur apporter.
* Que doivent-ils faire ensuite : inviter les utilisateurs à essayer une commande ou à interagir avec votre application.

Les messages d’accueil médiocres peuvent entraîner le blocage de votre bot par des utilisateurs. Écrivez au point et effacer les messages de bienvenue. Itérer sur les messages de bienvenue s’ils n’ont pas l’effet souhaité.

### <a name="notification-messages"></a>Les messages de notification

Pour envoyer des notifications à l’aide d’une messagerie proactive, assurez-vous que vos utilisateurs ont un chemin d’accès clair pour prendre des mesures communes en fonction de votre notification. Assurez-vous que les utilisateurs comprennent clairement pourquoi ils ont reçu une notification. Les messages de notification de bonne qualité incluent généralement les suivants :

* Ce qui s’est passé : une indication claire de ce qui est arrivé à l’origine de la notification.
* Résultat : il doit être clair sur quel élément a été mis à jour pour provoquer la notification.
* Qui ou ce qui l’a déclenché : Qui ou l’action qui a déclenché l’envoi de la notification.
* Que peuvent faire les utilisateurs en réponse : faciliter l’action de vos utilisateurs en fonction de vos notifications.
* Comment les utilisateurs peuvent-ils refuser : vous devez fournir un chemin d’accès aux utilisateurs pour qu’ils ne choisissent pas d’autres notifications.

Pour envoyer des messages à un grand groupe d’utilisateurs, par exemple à votre organisation, installez votre application de manière proactive à l’aide Graph.

### <a name="scheduled-messages"></a>Messages programmés

Lorsque vous utilisez une messagerie proactive pour envoyer des messages programmés aux utilisateurs, vérifiez que votre fuseau horaire est mis à jour vers leur fuseau horaire. Cela garantit que les messages sont remis aux utilisateurs au moment approprié. Les messages de planification incluent généralement :

* Pourquoi l’utilisateur reçoit-il le message : faciliter la compréhension de la raison pour laquelle il reçoit le message ?
* Que peut faire l’utilisateur ensuite : les utilisateurs peuvent prendre l’action requise en fonction du contenu du message.

## <a name="proactively-install-your-app-using-graph"></a>Installer votre application de manière proactive à l’aide Graph

> [!Note]
> L’installation proactive des applications à l Graph est actuellement en version bêta.

Envoyer un message de manière proactive aux utilisateurs qui n’ont pas précédemment installé ou interagi avec votre application. Par exemple, vous souhaitez utiliser le communicateur [d’entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation. Dans ce cas, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs. Mettre en cache les valeurs nécessaires à partir `conversationUpdate` de l’événement que votre application reçoit lors de l’installation.

Vous pouvez uniquement installer des applications qui se trouver dans votre catalogue d’applications d’organisation ou dans Teams App Store.

Voir [installer des applications pour les utilisateurs](/graph/api/userteamwork-post-installedapps) dans la documentation Graph et l’installation proactive du bot et la messagerie dans Teams avec [Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md). Il existe également un [exemple Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) sur la plateforme GitHub web.

## <a name="samples"></a>Exemples

Le code suivant présente un exemple de code simple qui installe de manière proactive votre application à l’aide Graph :

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
[Route("api/notify")]
[ApiController]
public class NotifyController : ControllerBase
{
    private readonly IBotFrameworkHttpAdapter _adapter;
    private readonly string _appId;
    private readonly ConcurrentDictionary<string, ConversationReference> _conversationReferences;

    public NotifyController(IBotFrameworkHttpAdapter adapter, IConfiguration configuration, ConcurrentDictionary<string, ConversationReference> conversationReferences)
    {
        _adapter = adapter;
        _conversationReferences = conversationReferences;
        _appId = configuration["MicrosoftAppId"] ?? string.Empty;
    }

    public async Task<IActionResult> Get()
    {
        foreach (var conversationReference in _conversationReferences.Values)
        {
            await ((BotAdapter)_adapter).ContinueConversationAsync(_appId, conversationReference, BotCallback, default(CancellationToken));
        }
        
        // Let the caller know proactive messages have been sent
        return new ContentResult()
        {
            Content = "<html><body><h1>Proactive messages have been sent.</h1></body></html>",
            ContentType = "text/html",
            StatusCode = (int)HttpStatusCode.OK,
        };
    }

    private async Task BotCallback(ITurnContext turnContext, CancellationToken cancellationToken)
    {
        // If you encounter permission-related errors when sending this message, see
        // https://aka.ms/BotTrustServiceUrl
        await turnContext.SendActivityAsync("proactive hello");
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

Vous devez fournir l’ID d’utilisateur et l’ID de client. Si l’appel réussit, l’API renvoie l’objet de réponse suivant :

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a>Exemple de code

Le tableau suivant fournit un exemple de code simple qui incorpore le flux de conversation de base dans une application Teams et comment créer un thread de conversation dans un canal dans Teams :

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Teams Informations de base sur les conversations  | Présente les principes de base des conversations Teams, notamment l’envoi de messages proactifs un-à-un.| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| Démarrer un nouveau thread dans un canal | Illustre la création d’un thread dans un canal. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

### <a name="additional-code-sample"></a>Exemple de code supplémentaire

> [!div class="nextstepaction"]
> [Teams exemples de code de messagerie proactifs](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [**Teams exemples de code de messagerie proactifs**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp) 
>  [Mettre en forme vos messages de bot](~/bots/how-to/format-your-bot-messages.md)
