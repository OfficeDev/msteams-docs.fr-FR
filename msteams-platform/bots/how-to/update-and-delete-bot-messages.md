---
title: Mettre à jour et supprimer les messages envoyés à partir de votre bot
author: WashingtonKayaker
description: Comment mettre à jour et supprimer des messages envoyés à partir de Microsoft Teams bot
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 90dc50fd2ec153813457f199ac029e17a0157502
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101533"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="2b10b-103">Mettre à jour et supprimer les messages envoyés à partir de votre bot</span><span class="sxs-lookup"><span data-stu-id="2b10b-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="2b10b-104">Votre bot peut mettre à jour dynamiquement les messages après les avoir envoyés au lieu de les avoir en tant que captures instantanées statiques des données.</span><span class="sxs-lookup"><span data-stu-id="2b10b-104">Your bot can dynamically update messages after sending them instead of having them as static snapshots of data.</span></span> <span data-ttu-id="2b10b-105">Les messages peuvent également être supprimés à l’aide de la méthode `DeleteActivity` Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="2b10b-105">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="update-messages"></a><span data-ttu-id="2b10b-106">Mettre à jour les messages</span><span class="sxs-lookup"><span data-stu-id="2b10b-106">Update messages</span></span>

<span data-ttu-id="2b10b-107">Vous pouvez utiliser les mises à jour dynamiques des messages pour des scénarios, tels que les mises à jour des sondages, la modification des actions disponibles après l’utilisation d’un bouton ou tout autre changement d’état asynchrone.</span><span class="sxs-lookup"><span data-stu-id="2b10b-107">You can use dynamic message updates for scenarios, such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="2b10b-108">Il n’est pas nécessaire que le nouveau message corresponde au type d’origine.</span><span class="sxs-lookup"><span data-stu-id="2b10b-108">It is not necessary for the new message to match the original in type.</span></span> <span data-ttu-id="2b10b-109">Par exemple, si le message d’origine contient une pièce jointe, le nouveau message peut être un message texte simple.</span><span class="sxs-lookup"><span data-stu-id="2b10b-109">For example, if the original message contains an attachment, the new message can be a simple text message.</span></span>

# <a name="c"></a>[<span data-ttu-id="2b10b-110">C#</span><span class="sxs-lookup"><span data-stu-id="2b10b-110">C#</span></span>](#tab/dotnet)

<span data-ttu-id="2b10b-111">Pour mettre à jour un message existant, passez un nouvel objet avec l’ID d’activité existant à la `Activity` `UpdateActivityAsync` méthode de la `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="2b10b-111">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="2b10b-112">Pour plus d’informations, [voir TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2b10b-112">For more information, see [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="2b10b-113">TypeScript</span><span class="sxs-lookup"><span data-stu-id="2b10b-113">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="2b10b-114">Pour mettre à jour un message existant, passez un nouvel objet avec l’ID d’activité existant à la `Activity` `updateActivity` méthode de `TurnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="2b10b-114">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="2b10b-115">Pour plus d’informations, voir [updateActivity.](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2b10b-115">For more information, see [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="2b10b-116">Python</span><span class="sxs-lookup"><span data-stu-id="2b10b-116">Python</span></span>](#tab/python)

<span data-ttu-id="2b10b-117">Pour mettre à jour un message existant, passez un nouvel objet avec l’ID d’activité existant à la `Activity` `update_activity` méthode de la `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="2b10b-117">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="2b10b-118">Voir [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2b10b-118">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="2b10b-119">API REST</span><span class="sxs-lookup"><span data-stu-id="2b10b-119">REST API</span></span>](#tab/rest)

> [!NOTE]

> <span data-ttu-id="2b10b-120">Vous pouvez développer des Teams dans n’importe quelle technologie de programmation web et appeler directement les API REST du [service Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2b10b-120">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="2b10b-121">Pour ce faire, vous [](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) devez implémenter des procédures de sécurité d’authentification avec vos demandes d’API.</span><span class="sxs-lookup"><span data-stu-id="2b10b-121">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="2b10b-122">Pour mettre à jour une activité existante au sein d’une conversation, incluez le point de terminaison de `conversationId` `activityId` la demande et celui-ci.</span><span class="sxs-lookup"><span data-stu-id="2b10b-122">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="2b10b-123">Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel post-courrier d’origine.</span><span class="sxs-lookup"><span data-stu-id="2b10b-123">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="2b10b-124">Demande</span><span class="sxs-lookup"><span data-stu-id="2b10b-124">Request</span></span> |<span data-ttu-id="2b10b-125">Réponse</span><span class="sxs-lookup"><span data-stu-id="2b10b-125">Response</span></span> |
|----|----|
| <span data-ttu-id="2b10b-126">Objet [Activity.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2b10b-126">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="2b10b-127">Objet [ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2b10b-127">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

---
* * *

<span data-ttu-id="2b10b-128">Maintenant que vous avez mis à jour les messages, mettez à jour la carte existante sur la sélection de bouton pour les activités entrantes.</span><span class="sxs-lookup"><span data-stu-id="2b10b-128">Now that you have updated messages, update the existing card on button selection for incoming activities.</span></span>

## <a name="update-cards"></a><span data-ttu-id="2b10b-129">Mettre à jour des cartes</span><span class="sxs-lookup"><span data-stu-id="2b10b-129">Update cards</span></span>

<span data-ttu-id="2b10b-130">Pour mettre à jour la carte existante sur la sélection de bouton, vous pouvez utiliser `ReplyToId` l’activité entrante.</span><span class="sxs-lookup"><span data-stu-id="2b10b-130">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="2b10b-131">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="2b10b-131">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="2b10b-132">Pour mettre à jour une carte existante sur une sélection de bouton, passez un nouvel objet avec carte mise à jour et en tant qu’ID d’activité à la méthode `Activity` `ReplyToId` de la `UpdateActivityAsync` `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="2b10b-132">To update existing card on a button selection, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="2b10b-133">Voir [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2b10b-133">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="2b10b-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="2b10b-134">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="2b10b-135">Pour mettre à jour une carte existante sur une sélection de bouton, passez un nouvel objet avec une carte mise à jour et en tant qu’ID d’activité à la méthode `Activity` `replyToId` de `updateActivity` `TurnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="2b10b-135">To update existing card on a button selection, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="2b10b-136">Voir [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2b10b-136">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="2b10b-137">Python</span><span class="sxs-lookup"><span data-stu-id="2b10b-137">Python</span></span>](#tab/python)

<span data-ttu-id="2b10b-138">Pour mettre à jour la carte existante sur un clic de bouton, passez un nouvel objet avec la carte mise à jour et en tant qu’ID d’activité à la méthode `Activity` `reply_to_id` de la `update_activity` `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="2b10b-138">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="2b10b-139">Voir [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2b10b-139">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="2b10b-140">API REST</span><span class="sxs-lookup"><span data-stu-id="2b10b-140">REST API</span></span>](#tab/rest)

> [!NOTE]
> <span data-ttu-id="2b10b-141">Vous pouvez développer des Teams dans n’importe quelle technologie de programmation web et appeler directement les API REST du service de [connecteur de bot.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2b10b-141">You can develop Teams apps in any web programming technology and directly call the [bot connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="2b10b-142">Pour ce faire, vous devez implémenter [des](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) procédures de sécurité d’authentification avec vos demandes d’API.</span><span class="sxs-lookup"><span data-stu-id="2b10b-142">To do this, you must implement [authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="2b10b-143">Pour mettre à jour une activité existante au sein d’une conversation, incluez le point de terminaison de `conversationId` `activityId` la demande et celui-ci.</span><span class="sxs-lookup"><span data-stu-id="2b10b-143">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="2b10b-144">Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel post-courrier d’origine.</span><span class="sxs-lookup"><span data-stu-id="2b10b-144">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="2b10b-145">Demande</span><span class="sxs-lookup"><span data-stu-id="2b10b-145">Request</span></span> |<span data-ttu-id="2b10b-146">Réponse</span><span class="sxs-lookup"><span data-stu-id="2b10b-146">Response</span></span> |
|----|----|
| <span data-ttu-id="2b10b-147">Objet [d’activité.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2b10b-147">An [activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="2b10b-148">Objet [ResourceResponse.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="2b10b-148">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

* * *

<span data-ttu-id="2b10b-149">Maintenant que vous avez mis à jour les cartes, vous pouvez supprimer des messages à l’aide de Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="2b10b-149">Now that you have updated cards, you can delete messages using the Bot Framework.</span></span>

## <a name="delete-messages"></a><span data-ttu-id="2b10b-150">Suppression de messages</span><span class="sxs-lookup"><span data-stu-id="2b10b-150">Delete messages</span></span>

<span data-ttu-id="2b10b-151">Dans Bot Framework, chaque message possède son identificateur d’activité unique.</span><span class="sxs-lookup"><span data-stu-id="2b10b-151">In the Bot Framework, every message has its unique activity identifier.</span></span> <span data-ttu-id="2b10b-152">Les messages peuvent être supprimés à l’aide de la méthode `DeleteActivity` Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="2b10b-152">Messages can be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

# <a name="c"></a>[<span data-ttu-id="2b10b-153">C#</span><span class="sxs-lookup"><span data-stu-id="2b10b-153">C#</span></span>](#tab/dotnet)

<span data-ttu-id="2b10b-154">Pour supprimer un message, passez l’ID de cette activité à `DeleteActivityAsync` la méthode de la `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="2b10b-154">To delete a message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="2b10b-155">Pour plus d’informations, [voir TurnContext.DeleteActivityAsync, méthode](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2b10b-155">For more information, see [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="2b10b-156">TypeScript</span><span class="sxs-lookup"><span data-stu-id="2b10b-156">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="2b10b-157">Pour supprimer un message, passez l’ID de cette activité à `deleteActivity` la méthode de `TurnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="2b10b-157">To delete a message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="2b10b-158">Pour plus d’informations, [voir deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="2b10b-158">For more information, see [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="2b10b-159">Python</span><span class="sxs-lookup"><span data-stu-id="2b10b-159">Python</span></span>](#tab/python)

<span data-ttu-id="2b10b-160">Pour supprimer ce message, passez l’ID de cette activité à `delete_activity` la méthode de `TurnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="2b10b-160">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="2b10b-161">Pour plus d’informations, [voir activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="2b10b-161">For more information, see [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="2b10b-162">API REST</span><span class="sxs-lookup"><span data-stu-id="2b10b-162">REST API</span></span>](#tab/rest)

<span data-ttu-id="2b10b-163">Pour supprimer une activité existante dans une conversation, incluez le point de terminaison de la `conversationId` `activityId` demande et celui-ci.</span><span class="sxs-lookup"><span data-stu-id="2b10b-163">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| <span data-ttu-id="2b10b-164">**Demande et réponse**</span><span class="sxs-lookup"><span data-stu-id="2b10b-164">**Request and response**</span></span> | <span data-ttu-id="2b10b-165">**Description**</span><span class="sxs-lookup"><span data-stu-id="2b10b-165">**Description**</span></span> |
|----|----|
| <span data-ttu-id="2b10b-166">S/O</span><span class="sxs-lookup"><span data-stu-id="2b10b-166">N/A</span></span> | <span data-ttu-id="2b10b-167">Code d’état HTTP indiquant le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="2b10b-167">An HTTP status code indicating the outcome of the operation.</span></span> <span data-ttu-id="2b10b-168">Rien n’est spécifié dans le corps de la réponse.</span><span class="sxs-lookup"><span data-stu-id="2b10b-168">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-sample"></a><span data-ttu-id="2b10b-169">Exemple de code</span><span class="sxs-lookup"><span data-stu-id="2b10b-169">Code sample</span></span>

<span data-ttu-id="2b10b-170">L’exemple de code suivant illustre les principes de base des conversations :</span><span class="sxs-lookup"><span data-stu-id="2b10b-170">The following code sample demonstrates basics of conversations:</span></span>

| <span data-ttu-id="2b10b-171">**Exemple de nom**</span><span class="sxs-lookup"><span data-stu-id="2b10b-171">**Sample name**</span></span> | <span data-ttu-id="2b10b-172">**Description**</span><span class="sxs-lookup"><span data-stu-id="2b10b-172">**Description**</span></span> | <span data-ttu-id="2b10b-173">**.NET**</span><span class="sxs-lookup"><span data-stu-id="2b10b-173">**.NET**</span></span> | <span data-ttu-id="2b10b-174">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="2b10b-174">**Node.js**</span></span> | <span data-ttu-id="2b10b-175">**Python**</span><span class="sxs-lookup"><span data-stu-id="2b10b-175">**Python**</span></span> |
|----------------------|-----------------|--------|-------------|--------|
| <span data-ttu-id="2b10b-176">Teams Informations de base sur les conversations</span><span class="sxs-lookup"><span data-stu-id="2b10b-176">Teams Conversation Basics</span></span>  | <span data-ttu-id="2b10b-177">Présente les principes de base des conversations Teams la mise à jour et la suppression des messages.</span><span class="sxs-lookup"><span data-stu-id="2b10b-177">Demonstrates basics of conversations in Teams including message update and delete.</span></span> | [<span data-ttu-id="2b10b-178">View</span><span class="sxs-lookup"><span data-stu-id="2b10b-178">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="2b10b-179">View</span><span class="sxs-lookup"><span data-stu-id="2b10b-179">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="2b10b-180">View</span><span class="sxs-lookup"><span data-stu-id="2b10b-180">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="2b10b-181">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="2b10b-181">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b10b-182">Obtenir Teams contexte</span><span class="sxs-lookup"><span data-stu-id="2b10b-182">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)
