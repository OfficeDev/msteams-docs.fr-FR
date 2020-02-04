---
title: Mettre à jour et supprimer des messages envoyés à partir de votre robot
author: WashingtonKayaker
description: Procédure de mise à jour et de suppression des messages envoyés à partir de votre robot Microsoft teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 012a6edb77f75c43cff01c58fb94e03fd4f61a85
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673923"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="e12cc-103">Mettre à jour et supprimer des messages envoyés à partir de votre robot</span><span class="sxs-lookup"><span data-stu-id="e12cc-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="e12cc-104">Mise à jour des messages</span><span class="sxs-lookup"><span data-stu-id="e12cc-104">Updating messages</span></span>

<span data-ttu-id="e12cc-105">Au lieu de faire en sorte que vos messages soient des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages après les avoir envoyés.</span><span class="sxs-lookup"><span data-stu-id="e12cc-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="e12cc-106">Vous pouvez utiliser les mises à jour de messages dynamiques pour des scénarios tels que les mises à jour de sondage, la modification des actions disponibles après une pression sur un bouton ou tout autre changement d’état asynchrone.</span><span class="sxs-lookup"><span data-stu-id="e12cc-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="e12cc-107">Le nouveau message n’a pas besoin de correspondre au type d’origine.</span><span class="sxs-lookup"><span data-stu-id="e12cc-107">The new message need not match the original in type.</span></span> <span data-ttu-id="e12cc-108">Par exemple, si le message d’origine contient une pièce jointe, le nouveau message peut être un simple message texte.</span><span class="sxs-lookup"><span data-stu-id="e12cc-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="e12cc-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e12cc-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="e12cc-110">Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `UpdateActivityAsync` activité existant à `TurnContext` la méthode de la classe.</span><span class="sxs-lookup"><span data-stu-id="e12cc-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="e12cc-111">*Voir* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="e12cc-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="e12cc-112">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="e12cc-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="e12cc-113">Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `updateActivity` activité existant à `TurnContext` la méthode de l’objet.</span><span class="sxs-lookup"><span data-stu-id="e12cc-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="e12cc-114">*Voir* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="e12cc-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="e12cc-115">Python</span><span class="sxs-lookup"><span data-stu-id="e12cc-115">Python</span></span>](#tab/python)

<span data-ttu-id="e12cc-116">Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `update_activity` activité existant à `TurnContext` la méthode de la classe.</span><span class="sxs-lookup"><span data-stu-id="e12cc-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="e12cc-117">Voir [TurnContextClass](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="e12cc-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a><span data-ttu-id="e12cc-118">Suppression de messages</span><span class="sxs-lookup"><span data-stu-id="e12cc-118">Deleting messages</span></span>

<span data-ttu-id="e12cc-119">Dans l’infrastructure bot, chaque message possède son propre identificateur d’activité unique.</span><span class="sxs-lookup"><span data-stu-id="e12cc-119">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="e12cc-120">Les messages peuvent être supprimés à l’aide de `DeleteActivity` la méthode de l’infrastructure bot, comme illustré ici.</span><span class="sxs-lookup"><span data-stu-id="e12cc-120">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="e12cc-121">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="e12cc-121">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="e12cc-122">Pour supprimer ce message, transmettez l’ID de cette activité `DeleteActivityAsync` à la méthode `TurnContext` de la classe.</span><span class="sxs-lookup"><span data-stu-id="e12cc-122">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="e12cc-123">*Voir* la [méthode TurnContext. DeleteActivityAsync](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="e12cc-123">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="e12cc-124">Machine à écrire/node. js</span><span class="sxs-lookup"><span data-stu-id="e12cc-124">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="e12cc-125">Pour supprimer ce message, transmettez l’ID de cette activité `deleteActivity` à la méthode `TurnContext` de l’objet.</span><span class="sxs-lookup"><span data-stu-id="e12cc-125">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="e12cc-126">*Voir* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="e12cc-126">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="pythontabpython"></a>[<span data-ttu-id="e12cc-127">Python</span><span class="sxs-lookup"><span data-stu-id="e12cc-127">Python</span></span>](#tab/python)

<span data-ttu-id="e12cc-128">Pour supprimer ce message, transmettez l’ID de cette activité `delete_activity` à la méthode `TurnContext` de l’objet.</span><span class="sxs-lookup"><span data-stu-id="e12cc-128">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="e12cc-129">Voir [delete_activity](link to Python API ref docs).</span><span class="sxs-lookup"><span data-stu-id="e12cc-129">See [delete_activity](link to Python API ref docs).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---

