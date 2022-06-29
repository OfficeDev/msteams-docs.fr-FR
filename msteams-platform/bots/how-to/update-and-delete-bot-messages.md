---
title: Mettre à jour et supprimer les messages envoyés à partir de votre bot
author: WashingtonKayaker
description: Découvrez comment mettre à jour et supprimer des messages envoyés à partir de votre bot Microsoft Teams dans différents environnements et avec des API REST à l’aide d’exemples de code.
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: bd52a3cfa27153c4349d50f4263dc29346fdfb45
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503801"
---
# <a name="update-and-delete-messages-sent-from-bot"></a>Mettre à jour et supprimer des messages envoyés à partir du bot 

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Votre bot peut mettre à jour dynamiquement les messages après les avoir envoyés au lieu de les avoir en tant qu’instantanés statiques de données. Les messages peuvent également être supprimés à l’aide de la méthode `DeleteActivity` du Bot Framework.

## <a name="update-messages"></a>Mettre à jour les messages

Vous pouvez utiliser des mises à jour de messages dynamiques pour des scénarios tels que les mises à jour de sondage, la modification des actions disponibles après une pression sur un bouton ou tout autre changement d’état asynchrone.

Il n’est pas nécessaire que le nouveau message corresponde au type d’origine. Par exemple, si le message d’origine contient une pièce jointe, le nouveau message peut être un message texte simple.

# <a name="c"></a>[C#](#tab/dotnet)

Pour mettre à jour un message existant, transmettez un nouvel objet `Activity` avec l’ID d’activité existant à la méthode `UpdateActivityAsync` de la classe `TurnContext`. Pour plus d’informations, consultez [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Pour mettre à jour un message existant, transmettez un nouvel objet `Activity` avec l’ID d’activité existant à la méthode `updateActivity` de l’objet `TurnContext`. Pour plus d’informations, consultez [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Pour mettre à jour un message existant, transmettez un nouvel objet `Activity` avec l’ID d’activité existant à la méthode `update_activity` de la classe `TurnContext`. Consultez [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[API REST](#tab/rest)

> [!NOTE]
> Vous pouvez développer des applications Teams dans n’importe quelle technologie de programmation web et appeler directement les [API REST du service Bot Connector](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true). Pour ce faire, vous devez mettre en œuvre des procédures de sécurité d'[authentification](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) avec vos demandes d'API.

Pour mettre à jour une activité existante dans une conversation, incluez les `conversationId` et `activityId` dans le point de terminaison de la requête. Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité retourné par l’appel de publication d’origine.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Demande |Réponse |
|----|----|
| Objet [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) . | Objet [ResourceResponse ](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true). |

---
---

Maintenant que vous avez mis à jour les messages, mettez à jour la carte existante lors de la sélection du bouton pour les activités entrantes.

## <a name="update-cards"></a>Mettre à jour les cartes

Pour mettre à jour la carte existante lors de la sélection du bouton, vous pouvez utiliser `ReplyToId` de l’activité entrante.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Pour mettre à jour la carte existante sur une sélection de bouton, transmettez un nouvel objet `Activity` avec la carte mise à jour et `ReplyToId` comme ID d’activité à la méthode `UpdateActivityAsync` de la classe `TurnContext` . Consultez [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Pour mettre à jour la carte existante sur une sélection de bouton, transmettez un nouvel objet `Activity` avec la carte mise à jour et `replyToId` comme ID d’activité à la méthode `updateActivity` de l’objet `TurnContext` . Consultez [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

Pour mettre à jour la carte existante sur un clic de bouton, passez un nouvel objet `Activity` avec la carte mise à jour et `reply_to_id` comme ID d’activité à la méthode `update_activity` de la classe `TurnContext` . Consultez [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[API REST](#tab/rest)

> [!NOTE]
> Vous pouvez développer des applications Teams dans n’importe quelle technologie de programmation web et appeler directement les [API REST du service de connecteur de bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true). Pour ce faire, vous devez implémenter [procédures d’authentification](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) de sécurité avec vos demandes d’API.

Pour mettre à jour une activité existante dans une conversation, incluez les `conversationId` et `activityId` dans le point de terminaison de la requête. Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité retourné par l’appel de publication d’origine.

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|Demande |Réponse |
|----|----|
| Objet [d’activité](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true). | Objet [ResourceResponse ](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true). |

---

Maintenant que vous avez mis à jour les cartes, vous pouvez supprimer des messages à l’aide de la Bot Framework.

## <a name="delete-messages"></a>Suppression de messages

Dans le Bot Framework, chaque message a son identificateur d’activité unique. Les messages peuvent être supprimés à l’aide de la méthode `DeleteActivity` du Bot Framework.

# <a name="c"></a>[C#](#tab/dotnet)

Pour supprimer un message, transmettez l’ID de cette activité à la méthode `DeleteActivityAsync` de la classe `TurnContext`. Pour plus d’informations, consultez [méthode TurnContext.DeleteActivityAsync](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

Pour supprimer un message, transmettez l’ID de cette activité à la méthode `deleteActivity` de l’objet `TurnContext`. Pour plus d’informations, consultez [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Pour supprimer ce message, transmettez l’ID de cette activité à la méthode `delete_activity` de l’objet `TurnContext`. Pour plus d’informations, consultez [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[API REST](#tab/rest)

Pour supprimer une activité existante dans une conversation, incluez les `conversationId` et `activityId` dans le point de terminaison de la demande.

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **Requête et réponse** | **Description** |
|----|----|
| S/O | Code d’état HTTP indiquant le résultat de l’opération. Rien n’est spécifié dans le corps de la réponse. |

---

## <a name="code-sample"></a>Exemple de code

L’exemple de code suivant illustre les concepts de base des conversations :

| **Exemple de nom** | **Description** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Informations de base des conversations Teams  | Présente les concepts de base des conversations dans Teams, notamment la mise à jour et la suppression des messages. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>Étape suivante

> [!div class="nextstepaction"]
> [obtenir des de contexte Teams](~/bots/how-to/get-teams-context.md)
