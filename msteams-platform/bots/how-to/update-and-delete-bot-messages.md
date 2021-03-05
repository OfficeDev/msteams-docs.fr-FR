---
title: Mettre à jour et supprimer les messages envoyés à partir de votre bot
author: WashingtonKayaker
description: Comment mettre à jour et supprimer des messages envoyés à partir de votre bot Microsoft Teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 664bd531bdee0093c6766bc23e35d2bf10307eb4
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449499"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="df04c-103">Mettre à jour et supprimer les messages envoyés à partir de votre bot</span><span class="sxs-lookup"><span data-stu-id="df04c-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="update-messages"></a><span data-ttu-id="df04c-104">Mettre à jour les messages</span><span class="sxs-lookup"><span data-stu-id="df04c-104">Update messages</span></span>

<span data-ttu-id="df04c-105">Votre bot peut mettre à jour dynamiquement les messages après les avoir envoyés.</span><span class="sxs-lookup"><span data-stu-id="df04c-105">Your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="df04c-106">Vous pouvez utiliser des mises à jour de messages dynamiques pour des scénarios tels que les mises à jour des sondages, la modification des actions disponibles après l’utilisation d’un bouton ou tout autre changement d’état asynchrone.</span><span class="sxs-lookup"><span data-stu-id="df04c-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="df04c-107">Le nouveau message ne doit pas nécessairement correspondre au type d’origine.</span><span class="sxs-lookup"><span data-stu-id="df04c-107">The new message need not match the original in type.</span></span> <span data-ttu-id="df04c-108">Par exemple, si le message d’origine contenait une pièce jointe, le nouveau message peut être un message texte simple.</span><span class="sxs-lookup"><span data-stu-id="df04c-108">For example, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="df04c-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="df04c-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="df04c-110">Pour mettre à jour un message existant, passez un nouvel objet avec l’ID d’activité existant à la `Activity` `UpdateActivityAsync` méthode de la `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="df04c-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="df04c-111">Voir [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="df04c-111">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="df04c-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="df04c-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="df04c-113">Pour mettre à jour un message existant, passez un nouvel objet avec l’ID d’activité existant à la `Activity` `updateActivity` méthode de `TurnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="df04c-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="df04c-114">Voir [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="df04c-114">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="df04c-115">Python</span><span class="sxs-lookup"><span data-stu-id="df04c-115">Python</span></span>](#tab/python)

<span data-ttu-id="df04c-116">Pour mettre à jour un message existant, passez un nouvel objet avec l’ID d’activité existant à la `Activity` `update_activity` méthode de la `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="df04c-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="df04c-117">Voir [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span><span class="sxs-lookup"><span data-stu-id="df04c-117">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="df04c-118">API REST</span><span class="sxs-lookup"><span data-stu-id="df04c-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="df04c-119">Vous pouvez développer des applications Teams dans n’importe quelle technologie de programmation web et appeler directement les API REST du [service Bot Connector.](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="df04c-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="df04c-120">Pour ce faire, vous [](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) devez implémenter des procédures de sécurité d’authentification avec vos demandes d’API.</span><span class="sxs-lookup"><span data-stu-id="df04c-120">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="df04c-121">Pour mettre à jour une activité existante dans une conversation, incluez le point de terminaison de `conversationId` `activityId` la demande et celui-ci.</span><span class="sxs-lookup"><span data-stu-id="df04c-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="df04c-122">Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel POST d’origine.</span><span class="sxs-lookup"><span data-stu-id="df04c-122">To complete this scenario, you must cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="df04c-123">**Corps de la demande**</span><span class="sxs-lookup"><span data-stu-id="df04c-123">**Request body**</span></span> | <span data-ttu-id="df04c-124">Objet [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="df04c-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object</span></span> |
| <span data-ttu-id="df04c-125">**Renvoie**</span><span class="sxs-lookup"><span data-stu-id="df04c-125">**Returns**</span></span> | <span data-ttu-id="df04c-126">Objet [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="df04c-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object</span></span> |

---

## <a name="update-cards"></a><span data-ttu-id="df04c-127">Mettre à jour des cartes</span><span class="sxs-lookup"><span data-stu-id="df04c-127">Update cards</span></span>

<span data-ttu-id="df04c-128">Pour mettre à jour la carte existante sur la sélection de bouton, vous pouvez utiliser `ReplyToId` l’activité entrante.</span><span class="sxs-lookup"><span data-stu-id="df04c-128">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="df04c-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="df04c-129">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="df04c-130">Pour mettre à jour la carte existante sur un clic de bouton, passez un nouvel objet avec carte mise à jour et en tant qu’ID d’activité à la méthode `Activity` `ReplyToId` de la `UpdateActivityAsync` `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="df04c-130">To update existing card on a button click, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="df04c-131">Voir [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="df04c-131">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>
```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="df04c-132">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="df04c-132">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="df04c-133">Pour mettre à jour la carte existante sur un clic de bouton, passez un nouvel objet avec une carte mise à jour et en tant qu’ID d’activité à la `Activity` `replyToId` méthode de `updateActivity` `TurnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="df04c-133">To update existing card on a button click, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="df04c-134">Voir [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="df04c-134">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>
```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="df04c-135">Python</span><span class="sxs-lookup"><span data-stu-id="df04c-135">Python</span></span>](#tab/python)

<span data-ttu-id="df04c-136">Pour mettre à jour la carte existante sur un clic de bouton, passez un nouvel objet avec carte mise à jour et en tant qu’ID d’activité à la méthode `Activity` `reply_to_id` de la `update_activity` `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="df04c-136">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="df04c-137">Voir [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span><span class="sxs-lookup"><span data-stu-id="df04c-137">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)

```

## <a name="delete-messages"></a><span data-ttu-id="df04c-138">Suppression de messages</span><span class="sxs-lookup"><span data-stu-id="df04c-138">Delete messages</span></span>

<span data-ttu-id="df04c-139">Dans Bot Framework, chaque message possède son propre identificateur d’activité unique.</span><span class="sxs-lookup"><span data-stu-id="df04c-139">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="df04c-140">Les messages peuvent être supprimés à l’aide de la méthode Bot `DeleteActivity` Framework, comme illustré ici.</span><span class="sxs-lookup"><span data-stu-id="df04c-140">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="df04c-141">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="df04c-141">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="df04c-142">Pour supprimer ce message, passez l’ID de cette activité à `DeleteActivityAsync` la méthode de la `TurnContext` classe.</span><span class="sxs-lookup"><span data-stu-id="df04c-142">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="df04c-143">Voir [TurnContext.DeleteActivityAsync, méthode](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="df04c-143">See [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="df04c-144">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="df04c-144">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="df04c-145">Pour supprimer ce message, passez l’ID de cette activité à `deleteActivity` la méthode de `TurnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="df04c-145">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="df04c-146">Voir [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="df04c-146">See [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="df04c-147">Python</span><span class="sxs-lookup"><span data-stu-id="df04c-147">Python</span></span>](#tab/python)

<span data-ttu-id="df04c-148">Pour supprimer ce message, passez l’ID de cette activité à `delete_activity` la méthode de `TurnContext` l’objet.</span><span class="sxs-lookup"><span data-stu-id="df04c-148">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="df04c-149">Voir [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="df04c-149">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="df04c-150">API REST</span><span class="sxs-lookup"><span data-stu-id="df04c-150">REST API</span></span>](#tab/rest)

 <span data-ttu-id="df04c-151">Pour supprimer une activité existante dans une conversation, incluez le point de terminaison de la `conversationId` `activityId` demande et celui-ci.</span><span class="sxs-lookup"><span data-stu-id="df04c-151">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="df04c-152">**Corps de la demande**</span><span class="sxs-lookup"><span data-stu-id="df04c-152">**Request body**</span></span> | <span data-ttu-id="df04c-153">s/o</span><span class="sxs-lookup"><span data-stu-id="df04c-153">n/a</span></span> |
| <span data-ttu-id="df04c-154">**Renvoie**</span><span class="sxs-lookup"><span data-stu-id="df04c-154">**Returns**</span></span> | <span data-ttu-id="df04c-155">Code d’état HTTP qui indique le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="df04c-155">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="df04c-156">Rien n’est spécifié dans le corps de la réponse.</span><span class="sxs-lookup"><span data-stu-id="df04c-156">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-samples"></a><span data-ttu-id="df04c-157">Exemples de code</span><span class="sxs-lookup"><span data-stu-id="df04c-157">Code samples</span></span>

<span data-ttu-id="df04c-158">Les principes de base de la conversation officielle sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="df04c-158">The official conversation basics are as follows:</span></span>

| <span data-ttu-id="df04c-159">Exemple de nom</span><span class="sxs-lookup"><span data-stu-id="df04c-159">Sample Name</span></span>           | <span data-ttu-id="df04c-160">Description</span><span class="sxs-lookup"><span data-stu-id="df04c-160">Description</span></span>                                                                      | <span data-ttu-id="df04c-161">.NET</span><span class="sxs-lookup"><span data-stu-id="df04c-161">.NET</span></span>    | <span data-ttu-id="df04c-162">JavaScript</span><span class="sxs-lookup"><span data-stu-id="df04c-162">JavaScript</span></span>   | <span data-ttu-id="df04c-163">Python</span><span class="sxs-lookup"><span data-stu-id="df04c-163">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="df04c-164">Informations de base sur les conversations Teams</span><span class="sxs-lookup"><span data-stu-id="df04c-164">Teams Conversation Basics</span></span>  | <span data-ttu-id="df04c-165">Présente les principes de base des conversations dans Teams, notamment la mise à jour et la suppression des messages.</span><span class="sxs-lookup"><span data-stu-id="df04c-165">Demonstrates basics of conversations in Teams, including message update and delete.</span></span>|[<span data-ttu-id="df04c-166">.NET &nbsp; Core</span><span class="sxs-lookup"><span data-stu-id="df04c-166">.NET&nbsp;Core</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="df04c-167">JavaScript</span><span class="sxs-lookup"><span data-stu-id="df04c-167">JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="df04c-168">Python</span><span class="sxs-lookup"><span data-stu-id="df04c-168">Python</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
