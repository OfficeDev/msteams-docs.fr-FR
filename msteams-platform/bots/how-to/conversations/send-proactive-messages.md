---
title: Envoyer des messages proactifs
description: Décrit l’envoi de messages proactifs à l’aide du bot Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: high
Keywords: envoyer un message obtenir l’identifiant utilisateur identification du canal identification de la conversation
ms.openlocfilehash: dc8c600c08c3f0e381a85aeef6c268ad8a5cbb96
ms.sourcegitcommit: 6906ba7e2a6e957889530b0a117a852c43bc86a6
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/24/2022
ms.locfileid: "63784008"
---
# <a name="proactive-messages"></a>Messages proactifs

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un message proactif est un message envoyé par un bot qui n'est pas en réponse à une demande d'un utilisateur. Il peut s'agir de messages tels que :

* Les messages de bienvenue
* Notifications
* Messages planifiés

Pour que votre bot envoie un message proactif à un utilisateur, une conversation de groupe ou d’équipe, il doit disposer d’accès pour envoyer le message. Pour une conversation de groupe ou d’équipe, l’application contenant votre bot doit d’abord être installée à cet emplacement.
Vous pouvez [installer votre application de manière proactive à l’aide de Microsoft Graph](#proactively-install-your-app-using-graph) dans une équipe, si nécessaire, ou utiliser une [stratégie d’application](/microsoftteams/teams-custom-app-policies-and-settings) pour la transmettre aux équipes et utilisateurs de votre client. Pour les utilisateurs, votre application doit être installée pour l’utilisateur ou votre utilisateur doit faire partie d’une équipe au sein de laquelle votre application est installée.

L’envoi d’un message proactif est différent de l’envoi d’un message classique. Il n’existe aucun `turnContext` actif à utiliser pour la réponse. Vous devez créer la conversation avant l’envoi du message. Par exemple, une nouvelle conversation individuelle ou un nouveau thread de conversation dans un canal. Vous ne pouvez pas créer une conversation de groupe ou un nouveau canal dans une équipe à l’aide d’une messagerie proactive.

Pour envoyer un message proactif, suivez ces étapes :

1. [Obtenez l’identifiant utilisateur, l’identification de l’équipe ou l’identification du canal](#get-the-user-id-team-id-or-channel-id) (si nécessaire).
1. [Créez la conversation](#create-the-conversation) (si nécessaire).
1. [Obtenez l’identification de la conversation](#get-the-conversation-id).
1. [Envoyez le message](#send-the-message).

Les extraits de code de la section [exemples](#samples) servent à la création d’une conversation individuelle. Pour obtenir des liens vers des exemples de tâches complets pour les conversations individuelles et les groupes ou canaux, voir [exemple de code](#code-sample).

Pour utiliser les messages proactifs de manière efficace, consultez les [Meilleures pratiques en matière de messagerie proactive](#best-practices-for-proactive-messaging). Dans certains cas, vous devez [installer votre application de manière proactive à l’aide de Graph](#proactively-install-your-app-using-graph). Les extraits de code de la section [exemples](#samples) servent à la création d’une conversation individuelle. Pour obtenir des exemples de tâches complets pour les conversations individuelles et les groupes ou canaux, voir [exemple de code](#code-sample).

## <a name="get-the-user-id-team-id-or-channel-id"></a>Obtenir l’identifiant utilisateur, l’identification de l’équipe ou l’identification du canal

Pour créer une conversation ou un thread de conversation dans un canal, vous devez avoir la correcte identification. Vous pouvez recevoir ou récupérer cette identification à l’aide de ce qui suit :

* Lorsque votre application est installée dans un contexte particulier, vous recevez une [`onMembersAdded`activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Lorsqu’un nouvel utilisateur est ajouté à un contexte où votre application est installée, vous recevez une [`onMembersAdded`activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Vous pouvez récupérer la [liste des canaux](~/bots/how-to/get-teams-context.md) d’une équipe où votre application est installée.
* Vous pouvez récupérer la [liste des membres](~/bots/how-to/get-teams-context.md) d’une équipe où votre application est installée.
* Chaque activité reçue par votre bot doit contenir les informations nécessaires.

Quelle que soit la façon dont vous obtenez les informations, vous devez stocker le `tenantId` et `userId` ou `channelId` pour créer une conversation. Vous pouvez également utiliser le `teamId` pour créer un thread de conversation dans le canal général ou par défaut d’une équipe.

Le `userId` est propre à votre identification de bot et à un utilisateur particulier. Vous ne pouvez pas réutiliser le `userId` entre les bots. Le `channelId` est global. Toutefois, vous devez installer votre bot dans l’équipe avant d’envoyer un message proactif à un canal.

Une fois que vous disposez des informations de l’utilisateur ou du canal, vous devez créer la conversation.

## <a name="create-the-conversation"></a>Créer la conversation

Vous devez créer la conversation si elle est inexistante ou si vous ne connaissez pas le `conversationId`. Vous ne devez créer la conversation qu’une seule fois et stocker la valeur `conversationId` ou l’objet `conversationReference`.

Une fois la conversation créée, vous devez obtenir l’identification de la conversation.

## <a name="get-the-conversation-id"></a>Obtenir l’identification de la conversation

Utilisez l’objet `conversationReference` ou `conversationId` et `tenantId` pour envoyer le message. Vous pouvez obtenir cette identification en créant la conversation ou en la stockant à partir de n’importe quelle activité vous étant envoyée à partir de ce contexte. Stockez cette identification pour référence.

Une fois les informations d’adresse appropriées reçues, vous pouvez envoyer votre message.

## <a name="send-the-message"></a>Envoyer le message

Maintenant que vous avez les bonnes informations relatives à l’adresse, vous pouvez envoyer votre message. Si vous utilisez le Kit de développement logiciel (SDK), vous devez utiliser la méthode `continueConversation`, ainsi que `conversationId` et `tenantId` pour effectuer un appel d’API direct. Vous devez correctement définir `conversationParameters` pour envoyer votre message. Consultez la section [exemples](#samples) ou utilisez l’un des exemples répertoriés dans la section [exemple de code](#code-sample).

Maintenant que vous avez envoyé le message proactif, vous devez suivre ces meilleures pratiques lors de l’envoi de messages proactifs pour améliorer l’échange d’informations entre les utilisateurs et le bot.

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques en matière de messagerie proactive

L’envoi de messages proactifs aux utilisateurs constitue un moyen de communication efficace avec vos utilisateurs. Toutefois, du point de vue des utilisateurs, le message s’affiche de manière spontanée. Lorsqu’il y a un message de bienvenue, il s’agira de leur première interaction avec votre application. Il est important d’utiliser cette fonctionnalité et de fournir des informations complètes à l’utilisateur pour comprendre l’objectif de ce message.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lorsque la messagerie proactive est utilisée pour envoyer un message de bienvenue à un utilisateur, il n’existe pas de contexte pour expliquer pourquoi les utilisateurs reçoivent le message. C’est également la première fois que les utilisateurs interagissent avec votre application. C’est l’opportunité de faire une bonne première impression. Les meilleurs messages de bienvenue doivent inclure :

* La raison pour laquelle l’utilisateur reçoit le message : l’utilisateur doit comprendre clairement pourquoi il reçoit le message. Si votre bot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal le bot a été installé et qui l’a installé.
* Ce que vous proposez : les utilisateurs doivent pouvoir identifier ce qu’ils peuvent faire avec votre application et la valeur que vous pouvez leur apporter.
* Que doivent-ils faire par la suite : invitez les utilisateurs à essayer une commande ou à interagir avec votre application.
Les messages d’accueil médiocres peuvent entraîner un blocage de votre bot par les utilisateurs. Écrivez des messages de bienvenue clairs et pertinents. Répétez les messages de bienvenue s’ils n’ont pas l’effet souhaité.

### <a name="notification-messages"></a>Les messages de notification

Pour envoyer des notifications à l’aide d’une messagerie proactive, vérifiez que vos utilisateurs ont un chemin d’accès clair pour prendre des mesures communes basées sur votre notification. Veillez à ce que les utilisateurs comprennent clairement pourquoi ils ont reçu une notification. Les messages de notification de bonne qualité incluent ce qui suit :

* Ce qui s’est produit : une indication claire de ce qui a causé la réception de la notification.
* Résultat : il doit être clair et indiquer quel élément est mis à jour pour recevoir la notification.
* La personne ou ce qui l’a déclenché : qui ou l’élément qui est intervenu ayant entraîné l’envoi de la notification.
* Ce que les utilisateurs peuvent faire en réponse : faciliter l’action de vos utilisateurs en fonction de vos notifications.
* Comment les utilisateurs peuvent-ils refuser les notifications : vous devez fournir un chemin d’accès aux utilisateurs afin qu’ils puissent désactiver les autres notifications.

Pour envoyer des messages à un grand groupe d’utilisateurs, par exemple à votre organisation, installez votre application de manière proactive en utilisation Graph.

### <a name="scheduled-messages"></a>Messages planifiés

Lorsque vous utilisez une messagerie proactive pour envoyer des messages planifiés aux utilisateurs, veillez à ce que votre fuseau horaire soit défini selon leur fuseau horaire. Cela garantit une remise des messages aux utilisateurs au moment pertinent. Les messages planifiés incluent généralement :

* Pourquoi l’utilisateur reçoit le message : permettez aux utilisateurs de comprendre facilement la raison pour laquelle ils reçoivent le message.
* Que peut faire l’utilisateur par la suite : les utilisateurs peuvent prendre les mesures nécessaires en fonction du contenu du message.

## <a name="proactively-install-your-app-using-graph"></a>Installer votre application de manière proactive en utilisant Graph

Envoyez de manière proactive un message aux utilisateurs qui n’ont pas précédemment installé ou interagi avec votre application. Par exemple, vous souhaitez utiliser le [communicateur d’entreprise](~/samples/app-templates.md#company-communicator) pour envoyer des messages à l’échelle de votre organisation. Dans ce cas, vous pouvez utiliser l’API Graph pour installer de manière proactive votre application pour vos utilisateurs. Mettez en cache les valeurs nécessaires à partir de l’événement `conversationUpdate` que votre application reçoit lors de l’installation.

Vous pouvez uniquement installer des applications figurant dans le catalogue des applications de votre organisation ou dans Teams de l’App Store.

Voir [installer des applications pour les utilisateurs](/graph/api/userteamwork-post-installedapps) dans la documentation Graph et [installation et messagerie proactive des bots dans Teams avec Graph](../../../graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md). Il existe également un [exemple .NET Framework Microsoft](https://github.com/microsoftgraph/contoso-airlines-teams-sample/blob/283523d45f5ce416111dfc34b8e49728b5012739/project/Models/GraphService.cs#L176) sur la plateforme GitHub.

## <a name="samples"></a>Échantillons

Le code suivant indique comment envoyer des messages proactifs :

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

Vous devez fournir l’identifiant utilisateur et l’identifiant du client. Si l’appel réussit, l’API renvoie l’objet de réponse suivant :

```json
{
  "id":"a:1qhNLqpUtmuI6U35gzjsJn7uRnCkW8NiZALHfN8AMxdbprS1uta2aT-jytfIlsZR3UZeg3TsIONNInBHsdjzj3PtfHuhkxxvS1jZZ61UAbw8fIdXcNSJyTJm7YvHFOgxo"
}
```

---

## <a name="code-sample"></a>Exemple de code

Le tableau suivant fournit un exemple de code simple qui incorpore un flux de conversation simple dans une application Teams et indique comment créer un thread de conversation dans un canal Teams :

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Informations de base des conversations Teams  | Présente les informations de base des conversations dans Teams, notamment l’envoi de messages individuels proactifs.| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| Démarrer un nouveau thread dans un canal | Présente la création d’un thread dans un canal. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |
| Installation proactive de l’application et envoi de notifications proactives | Cet exemple indique comment utiliser l’installation proactive de l’application pour les utilisateurs et envoyer des notifications proactives en appelant les API Microsoft Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) | |

### <a name="additional-code-sample"></a>Exemple de code supplémentaire

> [!div class="nextstepaction"]
> [Exemples de code Teams de messagerie proactive](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="step-by-step-guide"></a>Guide pas à pas

Suivez le [guide pas à pas](../../../sbs-send-proactive.yml) qui vous permet d’envoyer un message proactif à partir d’un bot.

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Formatez vos messages robots.](~/bots/how-to/format-your-bot-messages.md)

## <a name="see-also"></a>Voir aussi

* [**Exemples de code Teams de messagerie proactive**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
* [Conversations de canal et de groupe avec un bot](~/bots/how-to/conversations/channel-and-group-conversations.md)
* [Répondre à l’action d’envoi du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [Envoyer des notifications proactives aux utilisateurs](/azure/bot-service/bot-builder-howto-proactive-message)
