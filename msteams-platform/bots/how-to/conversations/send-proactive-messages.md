---
title: Envoyer des messages proactifs
description: Découvrez comment envoyer des messages proactifs avec votre bot Teams, installer votre application à l’aide de Microsoft Graph et vérifier des exemples de code basés sur le Kit de développement logiciel (SDK) Bot Framework v4.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 41c7d1ecd4c57bda98bb72dd66546df21fe74754
ms.sourcegitcommit: 024be23411bc0f2573d19f48f9266021f9b76f0d
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/31/2022
ms.locfileid: "67488263"
---
# <a name="proactive-messages"></a>Messages proactifs

[!INCLUDE [v4 to v3 pointer](~/includes/v4-to-v3-pointer-bots.md)]

Un message proactif est un message envoyé par un bot qui ne répond pas à la demande d’un utilisateur. Ce message peut inclure du contenu, par exemple :

* Les messages de bienvenue
* Notifications
* Messages planifiés

> [!IMPORTANT]
> Les bots sont disponibles dans government community cloud (GCC) et GCC-High, mais pas dans les environnements du ministère de la Défense (DOD).
>
> Pour les messages proactifs, les bots doivent utiliser les points de terminaison suivants pour les environnements cloud gouvernementaux :
>
> * Cloud de la communauté du secteur public : `https://smba.infra.gcc.teams.microsoft.com/gcc`.
> * GCCH : `https://smba.infra.gov.teams.microsoft.us/gcch`.

Pour envoyer un message proactif à un utilisateur, à une conversation de groupe ou à une équipe, votre bot doit disposer de l’accès requis pour envoyer le message. Pour une conversation de groupe ou d’équipe, l’application contenant votre bot doit d’abord être installée à cet emplacement.

Vous pouvez [installer votre application de manière proactive à l’aide de Microsoft Graph](#proactively-install-your-app-using-graph) dans une équipe, si nécessaire, ou utiliser une [stratégie d’application personnalisée](/microsoftteams/teams-custom-app-policies-and-settings) pour installer une application dans vos équipes et pour les utilisateurs de l’organisation. Dans certains cas, vous devez [installer votre application de manière proactive à l’aide de Graph](#proactively-install-your-app-using-graph). Pour qu’un utilisateur reçoive des messages proactifs, installez l’application pour l’utilisateur ou faites de l’utilisateur une partie d’une équipe dans laquelle l’application est installée.

L’envoi d’un message proactif est différent de l’envoi d’un message classique. Il n’existe aucun `turnContext` actif à utiliser pour la réponse. Vous devez créer la conversation avant l’envoi du message. Par exemple, une nouvelle conversation individuelle ou un nouveau thread de conversation dans un canal. Vous ne pouvez pas créer une conversation de groupe ou un nouveau canal dans une équipe à l’aide d’une messagerie proactive.

Pour envoyer un message proactif, suivez ces étapes :

1. [Obtenez l’identifiant utilisateur, l’identification de l’équipe ou l’identification du canal](#get-the-user-id-team-id-or-channel-id) (si nécessaire).
1. [Créez la conversation](#create-the-conversation) (si nécessaire).
1. [Obtenez l’identification de la conversation](#get-the-conversation-id).
1. [Envoyez le message](#send-the-message).

Les extraits de code de la section [Exemples](#samples) permettent de créer une conversation un-à-un. Pour obtenir des liens vers des exemples pour les conversations un-à-un et les messages de groupe ou de canaux, consultez [l’exemple de code](#code-sample). Pour utiliser efficacement des messages proactifs, consultez [les meilleures pratiques pour la messagerie proactive](#best-practices-for-proactive-messaging).

## <a name="get-the-user-id-team-id-or-channel-id"></a>Obtenir l’identifiant utilisateur, l’identification de l’équipe ou l’identification du canal

Pour créer une conversation ou un fil de conversation dans un canal, vous devez disposer de l’ID approprié. Vous pouvez recevoir ou récupérer cet ID de l’une des manières suivantes :

* Lorsque votre application est installée dans un contexte particulier, vous recevez une [`onMembersAdded` activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Lorsqu’un nouvel utilisateur est ajouté à un contexte où votre application est installée, vous recevez une [`onMembersAdded`activité](~/bots/how-to/conversations/subscribe-to-conversation-events.md).
* Chaque événement reçu par le bot contient les informations requises, que vous pouvez obtenir à partir du contexte du bot (objet TurnContext).
* Vous pouvez récupérer la [liste des canaux](~/bots/how-to/get-teams-context.md) d’une équipe où votre application est installée.
* Vous pouvez récupérer la [liste des membres](~/bots/how-to/get-teams-context.md) d’une équipe où votre application est installée.

Quelle que soit la façon dont vous obtenez les informations, stockez le `tenantId` ou les `userId` `channelId` éléments pour créer une conversation. Vous pouvez également utiliser le `teamId` pour créer un thread de conversation dans le canal général ou par défaut d’une équipe.

Le `userId` est propre à votre identification de bot et à un utilisateur particulier. Vous ne pouvez pas réutiliser le `userId` entre les bots. Le `channelId` est global. Toutefois, installez le bot dans l’équipe avant de pouvoir envoyer un message proactif à un canal.

Créez la conversation, une fois que vous avez les informations de l’utilisateur ou du canal.

## <a name="create-the-conversation"></a>Créer la conversation

Créez la conversation si elle n’existe pas ou si vous ne connaissez pas .`conversationId` Créez la conversation une seule fois et stockez la valeur ou `conversationReference` l’objet`conversationId`.

Vous pouvez obtenir la conversation lorsque l’application est installée pour la première fois. Une fois la conversation créée, [obtenez l’ID de conversation](#get-the-conversation-id). `conversationId` est disponible dans les événements de mise à jour de conversation.

Si vous n’en avez `conversationId`pas, vous pouvez [installer votre application de manière proactive à l’aide de Graph](#proactively-install-your-app-using-graph) pour obtenir le `conversationId`.

## <a name="get-the-conversation-id"></a>Obtenir l’identification de la conversation

Utilisez l’objet `conversationReference` ou `conversationId` et `tenantId` pour envoyer le message. Vous pouvez obtenir cette identification en créant la conversation ou en la stockant à partir de n’importe quelle activité vous étant envoyée à partir de ce contexte. Stockez cette identification pour référence.

Une fois les informations d’adresse appropriées reçues, vous pouvez envoyer votre message.

## <a name="send-the-message"></a>Envoyer le message

Maintenant que vous avez les bonnes informations relatives à l’adresse, vous pouvez envoyer votre message. Si vous utilisez le Kit de développement logiciel (SDK), vous devez utiliser la méthode `continueConversation`, ainsi que `conversationId` et `tenantId` pour effectuer un appel d’API direct. Pour envoyer votre message, définissez .`conversationParameters` Consultez la section [exemples](#samples) ou utilisez l’un des exemples répertoriés dans la section [exemple de code](#code-sample).

> [!NOTE]
> Teams ne prend pas en charge l’envoi de messages proactifs à l’aide d’un e-mail ou d’un nom d’utilisateur principal (UPN).

Maintenant que vous avez envoyé le message proactif, vous devez suivre ces meilleures pratiques lors de l’envoi de messages proactifs pour améliorer l’échange d’informations entre les utilisateurs et le bot.

Visionnez la vidéo suivante pour découvrir comment envoyer des messages proactifs à partir de bots :

<br>

> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4NHyk>]
<br>

### <a name="understand-who-blocked-muted-or-uninstalled-a-bot"></a>Comprendre qui a bloqué, désactivé ou désinstallé un bot

En tant que développeur, vous pouvez créer un rapport pour comprendre quels utilisateurs de votre organisation ont bloqué, désactivé ou désinstallé un bot. Ces informations peuvent aider les administrateurs de votre organisation à diffuser des messages à l’échelle de l’organisation ou à favoriser l’utilisation de l’application.

Avec Teams, vous pouvez envoyer un message proactif au bot pour vérifier si un utilisateur a bloqué ou désinstallé un bot. Si le bot est bloqué ou désinstallé, Teams retourne un `403` code de réponse avec un `subCode: MessageWritesBlocked`. Cette réponse indique que le message envoyé par le bot n’est pas remis à l’utilisateur.

Le code de réponse est envoyé par utilisateur et inclut l’identité de l’utilisateur. Vous pouvez compiler les codes de réponse de chaque utilisateur avec leur identité pour créer un rapport de tous les utilisateurs qui ont bloqué le bot.

Voici un exemple de code de réponse 403.

```http

HTTP/1.1 403 Forbidden

Cache-Control: no-store, must-revalidate, no-cache

 Pragma: no-cache

 Content-Length: 196

 Content-Type: application/json; charset=utf-8

 Server: Microsoft-HTTPAPI/2.0

 Strict-Transport-Security: max-age=31536000; includeSubDomains

 MS-CV: NXZpLk030UGsuHjPdwyhLw.5.0

 ContextId: tcid=0,server=msgapi-canary-eus2-0,cv=NXZpLk030UGsuHjPdwyhLw.5.0

 Date: Tue, 29 Mar 2022 17:34:33 GMT

{"errorCode":209,"message":"{\r\n  \"subCode\": \"MessageWritesBlocked\",\r\n  \"details\": \"Thread is blocked from message writes.\",\r\n  \"errorCode\": null,\r\n  \"errorSubCode\": null\r\n}"}
```

## <a name="best-practices-for-proactive-messaging"></a>Meilleures pratiques en matière de messagerie proactive

L’envoi de messages proactifs aux utilisateurs constitue un moyen de communication efficace avec vos utilisateurs. Toutefois, du point de vue des utilisateurs, le message s’affiche de manière spontanée. Lorsqu’il y a un message de bienvenue, il s’agira de leur première interaction avec votre application. Il est important d’utiliser cette fonctionnalité et de fournir des informations complètes à l’utilisateur pour comprendre l’objectif de ce message.

### <a name="welcome-messages"></a>Les messages de bienvenue

Lorsque la messagerie proactive est utilisée pour envoyer un message d’accueil à un utilisateur, il n’existe aucun contexte pour expliquer pourquoi l’utilisateur reçoit le message. En outre, il s’agit de la première interaction de l’utilisateur avec votre application. C’est l’opportunité de faire une bonne première impression. Une bonne expérience utilisateur garantit une meilleure adoption de l’application. Les messages d’accueil médiocres peuvent amener les utilisateurs à bloquer votre application. Écrivez un message d’accueil clair et itérer sur le message d’accueil s’il n’a pas l’effet souhaité.

Un bon message de bienvenue peut inclure les éléments suivants :

* Motif du message : il doit être clair pour l’utilisateur pourquoi il reçoit le message. Si votre robot a été installé dans un canal et que vous avez envoyé un message de bienvenue à tous les utilisateurs, faites-leur savoir dans quel canal il a été installé et qui l'a installé.

* Votre offre : les utilisateurs doivent être en mesure d’identifier ce qu’ils peuvent faire avec votre application et quelle valeur pouvez-vous leur apporter.

* Étapes suivantes : les utilisateurs doivent comprendre les étapes suivantes. Par exemple, invitez les utilisateurs à essayer une commande ou à interagir avec votre application.

### <a name="notification-messages"></a>Les messages de notification

Pour envoyer des notifications à l’aide d’une messagerie proactive, vérifiez que vos utilisateurs ont un chemin d’accès clair pour prendre des mesures communes basées sur votre notification. Veillez à ce que les utilisateurs comprennent clairement pourquoi ils ont reçu une notification. Les bons messages de notification incluent généralement les éléments suivants :

* Que s'est-il passé ? Une indication claire de ce qui a causé la réception de la notification.

* Quel a été le résultat? Il doit être clair et indiquer quel élément est mis à jour pour recevoir la notification.

* Qui ou ce qui l’a déclenché? Qui ou ce qui a pris des mesures, ce qui a provoqué l’envoi de la notification.

* Que peuvent faire les utilisateurs en réponse? Faciliter l’action de vos utilisateurs en fonction de vos notifications

* Comment les utilisateurs peuvent-ils refuser? Vous devez fournir un chemin d’accès pour permettre aux utilisateurs de refuser d’autres notifications.

Pour envoyer des messages à un grand groupe d’utilisateurs, par exemple à votre organisation, installez votre application de manière proactive en utilisation Graph.

### <a name="scheduled-messages"></a>Messages planifiés

Lorsque vous utilisez une messagerie proactive pour envoyer des messages planifiés aux utilisateurs, veillez à ce que votre fuseau horaire soit défini selon leur fuseau horaire. Cela garantit une remise des messages aux utilisateurs au moment pertinent. Les messages planifiés incluent généralement :

* Pourquoi l’utilisateur reçoit-il le message? Pour permettre aux utilisateurs de comprendre facilement la raison pour laquelle ils reçoivent le message

* Que peut faire l’utilisateur ensuite? Les utilisateurs peuvent prendre les mesures nécessaires en fonction du contenu du message.

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

Le tableau suivant fournit un exemple de code simple qui intègre le flux de conversation de base dans une application Teams et comment créer un nouveau fil de conversation dans un canal dans Teams :

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|---------------|--------------|--------|-------------|--------|
| Informations de base des conversations Teams  | Présente les informations de base des conversations dans Teams, notamment l’envoi de messages individuels proactifs.| [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/57.teams-conversation-bot) |
| Démarrer un nouveau thread dans un canal | Présente la création d’un thread dans un canal. | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/csharp_dotnetcore/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/javascript_nodejs/58.teams-start-new-thread-in-channel) | [View](https://github.com/microsoft/BotBuilder-Samples/blob/master/samples/python/58.teams-start-thread-in-channel) |
| Installation proactive de l’application et envoi de notifications proactives | Cet exemple indique comment utiliser l’installation proactive de l’application pour les utilisateurs et envoyer des notifications proactives en appelant les API Microsoft Graph. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-proactive-installation/nodejs) | |
| Messagerie proactive | Il s’agit d’un exemple qui montre comment enregistrer les informations de référence de conversation de l’utilisateur pour envoyer un message de rappel proactif à l’aide de Bots. | Bientôt disponible | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging-teamsfx) | - |

> [!div class="nextstepaction"]
> [Exemple de code supplémentaire de messagerie proactive](/samples/officedev/msteams-samples-proactive-messaging/msteams-samples-proactive-messaging/)

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Formatez vos messages robots.](~/bots/how-to/format-your-bot-messages.md)

## <a name="see-also"></a>Voir aussi

* [**Exemples de code Teams de messagerie proactive**](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-proactive-messaging/csharp)
* [Conversations de canal et de groupe avec un bot](~/bots/how-to/conversations/channel-and-group-conversations.md)
* [Répondre à l’action d’envoi du module de tâche](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)
* [Envoyer des notifications proactives aux utilisateurs](/azure/bot-service/bot-builder-howto-proactive-message)
* [Créer votre première application de bot à l’aide de JavaScript](../../../sbs-gs-bot.yml)
* [Créer un bot de notification avec JavaScript pour envoyer un message proactif](../../../sbs-gs-notificationbot.yml)
* [TurnContext](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest"&preserve-view=true")
