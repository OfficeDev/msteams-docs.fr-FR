---
title: Mettre à jour et supprimer des messages envoyés à partir de votre robot
author: WashingtonKayaker
description: Procédure de mise à jour et de suppression des messages envoyés à partir de votre robot Microsoft teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 46994c6810197002ef1c108af4f725426395b37f
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2020
ms.locfileid: "43957186"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="f1cfe-103">Mettre à jour et supprimer des messages envoyés à partir de votre robot</span><span class="sxs-lookup"><span data-stu-id="f1cfe-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="f1cfe-104">Mise à jour des messages</span><span class="sxs-lookup"><span data-stu-id="f1cfe-104">Updating messages</span></span>

<span data-ttu-id="f1cfe-105">Au lieu de faire en sorte que vos messages soient des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages après les avoir envoyés.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="f1cfe-106">Vous pouvez utiliser les mises à jour de messages dynamiques pour des scénarios tels que les mises à jour de sondage, la modification des actions disponibles après une pression sur un bouton ou tout autre changement d’état asynchrone.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="f1cfe-107">Le nouveau message n’a pas besoin de correspondre au type d’origine.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-107">The new message need not match the original in type.</span></span> <span data-ttu-id="f1cfe-108">Par exemple, si le message d’origine contient une pièce jointe, le nouveau message peut être un simple message texte.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1cfe-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1cfe-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f1cfe-110">Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `UpdateActivityAsync` activité existant à `TurnContext` la méthode de la classe.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="f1cfe-111">*Voir* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="f1cfe-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1cfe-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1cfe-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="f1cfe-113">Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `updateActivity` activité existant à `TurnContext` la méthode de l’objet.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f1cfe-114">*Voir* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="f1cfe-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="f1cfe-115">Python</span><span class="sxs-lookup"><span data-stu-id="f1cfe-115">Python</span></span>](#tab/python)

<span data-ttu-id="f1cfe-116">Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `update_activity` activité existant à `TurnContext` la méthode de la classe.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="f1cfe-117">Voir [TurnContextClass](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="f1cfe-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="f1cfe-118">API REST</span><span class="sxs-lookup"><span data-stu-id="f1cfe-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="f1cfe-119">Vous pouvez développer des applications teams dans n’importe quelle technologie de programmation Web et appeler directement les [API REST du service du connecteur bot](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0).</span><span class="sxs-lookup"><span data-stu-id="f1cfe-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0).</span></span> <span data-ttu-id="f1cfe-120">Pour ce faire, vous devez implémenter les procédures de sécurité [d’authentification](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) avec vos demandes d’API.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-120">To do so, you'll need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) security procedures with your API requests.</span></span>

<span data-ttu-id="f1cfe-121">Pour mettre à jour une activité existante au sein d’une `conversationId` conversation `activityId` , incluez le et dans le point de terminaison de la demande.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="f1cfe-122">Pour effectuer ce scénario, vous devez mettre en cache l’ID d’activité renvoyé par l’appel POST d’origine.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-122">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="f1cfe-123">**Corps de la demande**</span><span class="sxs-lookup"><span data-stu-id="f1cfe-123">**Request body**</span></span> | <span data-ttu-id="f1cfe-124">Un objet [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object)</span><span class="sxs-lookup"><span data-stu-id="f1cfe-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object) object</span></span> |
| <span data-ttu-id="f1cfe-125">**Renvoie**</span><span class="sxs-lookup"><span data-stu-id="f1cfe-125">**Returns**</span></span> | <span data-ttu-id="f1cfe-126">Objet [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object)</span><span class="sxs-lookup"><span data-stu-id="f1cfe-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object) object</span></span> |

---

## <a name="deleting-messages"></a><span data-ttu-id="f1cfe-127">Suppression de messages</span><span class="sxs-lookup"><span data-stu-id="f1cfe-127">Deleting messages</span></span>

<span data-ttu-id="f1cfe-128">Dans l’infrastructure bot, chaque message possède son propre identificateur d’activité unique.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-128">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="f1cfe-129">Les messages peuvent être supprimés à l’aide de `DeleteActivity` la méthode de l’infrastructure bot, comme illustré ici.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-129">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="f1cfe-130">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="f1cfe-130">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="f1cfe-131">Pour supprimer ce message, transmettez l’ID de cette activité `DeleteActivityAsync` à la méthode `TurnContext` de la classe.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-131">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="f1cfe-132">*Voir* la [méthode TurnContext. DeleteActivityAsync](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="f1cfe-132">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="f1cfe-133">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="f1cfe-133">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="f1cfe-134">Pour supprimer ce message, transmettez l’ID de cette activité `deleteActivity` à la méthode `TurnContext` de l’objet.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-134">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f1cfe-135">*Voir* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="f1cfe-135">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="f1cfe-136">Python</span><span class="sxs-lookup"><span data-stu-id="f1cfe-136">Python</span></span>](#tab/python)

<span data-ttu-id="f1cfe-137">Pour supprimer ce message, transmettez l’ID de cette activité `delete_activity` à la méthode `TurnContext` de l’objet.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-137">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="f1cfe-138">Voir [Activity-Update-and-Delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span><span class="sxs-lookup"><span data-stu-id="f1cfe-138">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="f1cfe-139">API REST</span><span class="sxs-lookup"><span data-stu-id="f1cfe-139">REST API</span></span>](#tab/rest)

 <span data-ttu-id="f1cfe-140">Pour supprimer une activité existante au sein d’une conversation, `conversationId` incluez le et `activityId` dans le point de terminaison de la demande.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-140">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="f1cfe-141">**Corps de la demande**</span><span class="sxs-lookup"><span data-stu-id="f1cfe-141">**Request body**</span></span> | <span data-ttu-id="f1cfe-142">s/o</span><span class="sxs-lookup"><span data-stu-id="f1cfe-142">n/a</span></span> |
| <span data-ttu-id="f1cfe-143">**Renvoie**</span><span class="sxs-lookup"><span data-stu-id="f1cfe-143">**Returns**</span></span> | <span data-ttu-id="f1cfe-144">Un code d’état HTTP qui indique le résultat de l’opération.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-144">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="f1cfe-145">Nothing est spécifié dans le corps de la réponse.</span><span class="sxs-lookup"><span data-stu-id="f1cfe-145">Nothing is specified in the body of the response.</span></span> |

---
