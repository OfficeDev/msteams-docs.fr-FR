---
title: Mettre à jour et supprimer les messages envoyés à partir de votre bot
author: WashingtonKayaker
description: Découvrez comment mettre à jour et supprimer des messages envoyés à partir de votre bot Microsoft Teams dans différents environnements et avec des API REST à l’aide d’exemples de code.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: b02e4ec19fdb3494ef4e84e4f8de1ba25645f91a
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453725"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Mettre à jour et supprimer les messages envoyés à partir de votre bot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Votre bot peut mettre à jour dynamiquement les messages après les avoir envoyés au lieu de les avoir en tant que captures instantanées statiques des données. Les messages peuvent également être supprimés à l’aide de la méthode `DeleteActivity` Bot Framework.

## <a name="update-messages"></a>Mettre à jour les messages

Vous pouvez utiliser les mises à jour dynamiques des messages pour des scénarios, tels que les mises à jour des sondages, la modification des actions disponibles après l’utilisation d’un bouton ou tout autre changement d’état asynchrone.

Il n’est pas nécessaire que le nouveau message corresponde au type d’origine. Par exemple, si le message d’origine contient une pièce jointe, le nouveau message peut être un message texte simple.

# <a name="c"></a>[C#](#tab/dotnet)

Pour mettre à jour un message existant, passez `Activity` un nouvel objet avec l’ID d’activité existant à `UpdateActivityAsync` la méthode de la `TurnContext` classe. Pour plus d’informations, [voir TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Pour mettre à jour un message existant, passez `Activity` un nouvel objet avec l’ID d’activité existant à `updateActivity` la méthode de l’objet `TurnContext` . Pour plus d’informations, [voir updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Pour mettre à jour un message existant, passez `Activity` un nouvel objet avec l’ID d’activité existant à `update_activity` la méthode de la `TurnContext` classe. Voir [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[API REST](#tab/rest)

> [!NOTE]
> Vous pouvez développer des Teams dans n’importe quelle technologie de programmation web et appeler directement les [API REST du service Bot Connector](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true). Pour ce faire, vous devez implémenter des procédures de sécurité d’authentification avec vos demandes d’API.[](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true)

Pour mettre à jour une activité existante au sein d’une conversation, incluez le `conversationId` `activityId` point de terminaison de la demande et celui-ci. Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel post-courrier d’origine.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Demande |Réponse |
|----|----|
| Objet [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) . | Objet [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) . |

---
---

Maintenant que vous avez mis à jour les messages, mettez à jour la carte existante sur la sélection de bouton pour les activités entrantes.

## <a name="update-cards"></a>Mettre à jour des cartes

Pour mettre à jour la carte existante sur la sélection de bouton, vous pouvez utiliser l’activité `ReplyToId` entrante.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Pour mettre à jour une carte existante sur une sélection de bouton, `Activity` `ReplyToId` passez un nouvel objet avec carte mise à jour et en tant qu’ID `UpdateActivityAsync` d’activité à la méthode de la `TurnContext` classe. Voir [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Pour mettre à jour une carte existante sur une sélection de bouton, `Activity` `replyToId` passez un nouvel objet avec carte mise à jour et en tant qu’ID `updateActivity` d’activité à la méthode de l’objet `TurnContext` . Voir [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

Pour mettre à jour la carte existante sur un clic de bouton, `Activity` `reply_to_id` passez un nouvel objet avec carte mise à jour et en tant qu’ID `update_activity` d’activité à la méthode de la `TurnContext` classe. Voir [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[API REST](#tab/rest)

> [!NOTE]
> Vous pouvez développer des Teams dans n’importe quelle technologie de programmation web et appeler directement les [API REST du service connecteur de bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true). Pour ce faire, vous devez implémenter [des](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) procédures de sécurité d’authentification avec vos demandes d’API.

Pour mettre à jour une activité existante au sein d’une conversation, incluez le `conversationId` `activityId` point de terminaison de la demande et celui-ci. Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel post-courrier d’origine.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Demande |Réponse |
|----|----|
| Objet [d’activité](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) . | Objet [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) . |

---

Maintenant que vous avez mis à jour les cartes, vous pouvez supprimer des messages à l’aide de Bot Framework.

## <a name="delete-messages"></a>Suppression de messages

Dans Bot Framework, chaque message possède son identificateur d’activité unique. Les messages peuvent être supprimés à l’aide de la méthode `DeleteActivity` Bot Framework.

# <a name="c"></a>[C#](#tab/dotnet)

Pour supprimer un message, passez l’ID de cette activité à la `DeleteActivityAsync` méthode de la `TurnContext` classe. Pour plus d’informations, [voir TurnContext.DeleteActivityAsync, méthode](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Pour supprimer un message, passez l’ID de cette activité à la `deleteActivity` méthode de l’objet `TurnContext` . Pour plus d’informations, [voir deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Pour supprimer ce message, passez l’ID de cette activité à la `delete_activity` méthode de l’objet `TurnContext` . Pour plus d’informations, [voir activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[API REST](#tab/rest)

Pour supprimer une activité existante dans une conversation, incluez le `conversationId` `activityId` point de terminaison de la demande et celui-ci.

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **Demande et réponse** | **Description** |
|----|----|
| N/A | Code d’état HTTP indiquant le résultat de l’opération. Rien n’est spécifié dans le corps de la réponse. |

---

## <a name="code-sample"></a>Exemple de code

L’exemple de code suivant illustre les principes de base des conversations :

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Informations de base des conversations Teams  | Présente les principes de base des conversations Teams la mise à jour et la suppression des messages. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [Obtenir Teams contexte](~/bots/how-to/get-teams-context.md)
