---
title: envoyer des messages proactifs
description: explique comment envoyer des messages proactifs avec votre bot Microsoft Teams.
ms.topic: overview
ms.author: anclear
Keywords: envoyer un message pour obtenir l’ID de conversation de l’ID de canal de l’ID de l’utilisateur
ms.openlocfilehash: 2d7ff10469a181bb06fda5029c8f6b2725b0402d
ms.sourcegitcommit: 7db6eabe3ef128ac7f14b32d07e9e86c995d187f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/04/2021
ms.locfileid: "50103604"
---
# <a name="send-proactive-messages"></a>Envoi de messages proactifs

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un message proactif est un message envoyé par un bot qui n’est pas en réponse directe à une demande d’un utilisateur. Cela peut inclure des messages tels que :

* Les messages de bienvenue
* Notifications
* Messages programmés

Pour que votre bot envoie un message proactif, il doit avoir accès à l’utilisateur, à la conversation de groupe ou à l’équipe à qui vous souhaitez envoyer le message. Pour une conversation de groupe ou une équipe, cela signifie que l’application qui contient votre bot doit d’abord être installée à cet emplacement. Vous pouvez [installer votre](#proactively-install-your-app-using-graph) application de manière proactive à [](/microsoftteams/teams-custom-app-policies-and-settings) l’aide de Graph dans une équipe, si nécessaire, ou utiliser une stratégie d’application pour faire sortir les applications vers les équipes et les utilisateurs de votre client. Pour les utilisateurs, votre application doit être installée pour l’utilisateur ou votre utilisateur doit faire partie d’une équipe sur laquelle votre application est installée.

L’envoi d’un message proactif est différent de l’envoi d’un message normal. Dans ce cas, il n’est pas actif `turnContext` à utiliser pour une réponse. Vous devrez peut-être également créer la conversation avant d’envoyer le message. Par exemple, une nouvelle conversation un-à-un ou un nouveau thread de conversation dans un canal. Vous ne pouvez pas créer une conversation de groupe ou un nouveau canal dans une équipe avec une messagerie proactive.

À un niveau élevé, les étapes à suivre pour envoyer un message proactif sont les suivantes :

1. [Obtenez l’ID utilisateur ou l’ID d’équipe/canal](#get-the-user-id-or-teamchannel-id) (si nécessaire).
1. [Créez la conversation ou le thread de conversation](#create-the-conversation) (si nécessaire).
1. [Obtenir l’ID de conversation](#get-the-conversation-id).
1. [Envoyer le message](#send-the-message).

Les extraits de code de la section [Exemples](#examples) sont pour la création d’une conversation un-à-un. Pour obtenir des liens vers des exemples de travail complets pour les conversations un-à-un et les groupes ou canaux, voir [les exemples de code.](#code-samples)

## <a name="get-the-user-id-or-teamchannel-id"></a>Obtenir l’ID utilisateur ou l’ID d’équipe/canal

Pour créer une conversation ou un thread de conversation dans un canal, vous avez besoin de l’ID correct. Vous pouvez recevoir ou récupérer cet ID de plusieurs manières :

1. Lorsque votre application est installée dans un contexte particulier, vous recevez une [ `onMembersAdded` activité.](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
1. Lorsqu’un nouvel utilisateur est ajouté à un contexte où votre application est installée, vous recevez une [ `onMembersAdded` activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
1. Vous pouvez récupérer la [liste des canaux](~/bots/how-to/get-teams-context.md) dans une équipe où votre application est installée.
1. Vous pouvez récupérer la [liste des membres d’une](~/bots/how-to/get-teams-context.md) équipe sur l’installation de votre application.
1. Chaque activité que reçoit votre bot doit contenir les informations requises.

Quelle que soit la façon dont vous gagnez les informations, vous devez stocker les informations et créer ou créer `tenantId` `userId` une `channelId` conversation. Vous pouvez également l’utiliser pour créer un thread de conversation dans le canal général ou `teamId` par défaut d’une équipe.

Il est propre à votre ID de bot et à un utilisateur particulier, vous ne pouvez pas `userId` les ré-utiliser entre les bots. La stratégie globale, toutefois, votre bot doit être installé dans l’équipe avant de pouvoir envoyer un `channelId` message proactif à un canal.

## <a name="create-the-conversation"></a>Créer la conversation

Une fois que vous avez les informations de l’utilisateur ou du canal, vous devez créer la conversation si elle n’existe pas déjà ou si vous ne connaissez pas le `conversationId` . Vous ne devez créer la conversation qu’une seule fois et vous assurer de stocker la valeur ou `conversationId` l’objet à utiliser à `conversationReference` l’avenir.

## <a name="get-the-conversation-id"></a>Obtenir l’ID de conversation

Une fois la conversation créée, utilisez l’objet ou pour `conversationReference` `conversationId` envoyer le `tenantId` message. Vous pouvez obtenir cet ID en créant la conversation ou en la stockant à partir de n’importe quelle activité qui vous est envoyée à partir de ce contexte. Assurez-vous de stocker cet ID.

## <a name="send-the-message"></a>Envoyer le message

Maintenant que vous avez les bonnes informations d’adresse, vous pouvez envoyer votre message. Si vous utilisez le SDK, vous devez utiliser la méthode et effectuer un appel `continueConversation` `conversationId` `tenantId` d’API direct. Vous devez définir correctement `conversationParameters` l’envoi de votre message. Consultez la section [exemples](#examples) ou utilisez l’un des exemples répertoriés dans la section [exemples de](#code-samples) code.

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques en matière de messagerie proactive

L’envoi de messages proactifs aux utilisateurs est un moyen très efficace de communiquer avec vos utilisateurs. Toutefois, de leur point de vue, ce message peut apparaître complètement non improvisé et, dans le cas des messages de bienvenue, c’est la première fois qu’ils interagissent avec votre application. Par conséquent, il est très important d’utiliser cette fonctionnalité avec parcimonie, de ne pas envoyer de courrier indésirable à vos utilisateurs et de fournir suffisamment d’informations pour que les utilisateurs comprennent pourquoi ils sont envoyés par message.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lorsque vous utilisez une messagerie proactive pour envoyer un message de bienvenue à un utilisateur, vous devez garder à l’esprit que, pour la plupart des personnes qui reçoivent le message, il n’existe aucun contexte pour la raison pour laquelle elles le reçoivent. C’est également la première fois qu’ils interagissent avec votre application. C’est l’occasion de créer une bonne première impression. Les meilleurs messages de bienvenue doivent être les suivants :

* **Pourquoi un utilisateur reçoit le message .** Il doit être très clair pour l’utilisateur pourquoi il reçoit le message. Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et éventuellement qui l’a installé.
* **Que proposez-vous ?** Que peuvent-ils faire avec votre application ? Quelle valeur pouvez-vous leur apporter ?
* **Que doivent-ils faire ensuite ?** Invitez-les à essayer une commande ou à interagir avec votre application d’une certaine façon.

N’oubliez pas que des messages d’accueil médiocres peuvent entraîner le blocage de votre bot par des utilisateurs. Passez beaucoup de temps à créer vos messages de bienvenue et à les itérer s’ils n’ont pas l’effet souhaité.

### <a name="notification-messages"></a>Les messages de notification

Lorsque vous utilisez une messagerie proactive pour envoyer des notifications, vous devez vous assurer que vos utilisateurs ont un chemin d’accès clair pour prendre des mesures communes en fonction de votre notification et comprendre clairement pourquoi la notification s’est produite. Les messages de notification de bonne qualité sont généralement les suivants :

* **Que s'est-il passé.** Indication claire de ce qui est arrivé à l’origine de la notification.
* **Quel a été le résultat.** Il doit être clair quel élément ou élément a été mis à jour pour provoquer la notification.
* **Qui/ce qui l’a déclenché.** Qui ou quelle action a été à l’origine de l’envoi de la notification.
* **Que peuvent faire les utilisateurs en réponse ?** Faites en sorte que vos utilisateurs prennent facilement des mesures en fonction de vos notifications.
* **Comment les utilisateurs peuvent-ils refuser ?** Vous devez fournir un chemin d’accès aux utilisateurs pour qu’ils ne choisissent pas d’autres notifications.

## <a name="proactively-install-your-app-using-graph"></a>Installer votre application de manière proactive à l’aide de Graph

> [!Note]
> L’installation proactive d’applications à l’aide de Microsoft Graph est actuellement en version bêta.

Parfois, il peut s’agir d’un message de manière proactive pour les utilisateurs qui n’ont pas installé votre application ou qui n’ont jamais interagi avec celle-ci. Par exemple, vous souhaitez utiliser le communicateur [d’entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’ensemble de votre organisation. Pour ce scénario, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs, puis mettre en cache les valeurs nécessaires à partir de l’événement que votre application reçoit lors de `conversationUpdate` l’installation.

Vous pouvez uniquement installer des applications qui se trouver dans votre catalogue d’applications d’organisation ou dans le magasin d’applications Teams.

Voir [Installer des applications pour les utilisateurs](/graph/api/userteamwork-post-installedapps) dans la documentation Graph et l’installation proactive du bot et la messagerie dans Teams avec Microsoft [Graph.](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md) Il existe également un [exemple Microsoft .NET Framework](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) sur la plateforme GitHub.

## <a name="examples"></a>Exemples

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

## <a name="code-samples"></a>Exemples de code

Les exemples de messagerie proactive officiels sont les suivants :

| Exemple de nom           | Description                                                                      | .NET    | JavaScript   | Python  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|Informations de base sur les conversations Teams  | Présente les principes de base des conversations dans Teams, notamment l’envoi de messages proactifs un-à-un.|[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot)|
|Démarrer un nouveau thread dans un canal     | Illustre la création d’un thread dans un canal. |[.NET &nbsp; Core](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel)|[JavaScript](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel)|[Python](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |

## <a name="view-additional-code-samples"></a>Afficher des exemples de code supplémentaires
>
> [!div class="nextstepaction"]
> [**Exemples de code de messagerie proactive Teams**](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)
>
