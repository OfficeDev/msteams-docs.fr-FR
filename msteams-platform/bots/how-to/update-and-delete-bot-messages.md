---
title: Mettre à jour et supprimer des messages envoyés à partir de votre robot
author: WashingtonKayaker
description: Procédure de mise à jour et de suppression des messages envoyés à partir de votre robot Microsoft teams
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 222409fa0d02a571b7295dedb0c60b1ca3f90cca
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914608"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>Mettre à jour et supprimer des messages envoyés à partir de votre robot

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a>Mise à jour des messages

Au lieu de faire en sorte que vos messages soient des instantanés statiques de données, votre bot peut mettre à jour dynamiquement les messages après les avoir envoyés. Vous pouvez utiliser les mises à jour de messages dynamiques pour des scénarios tels que les mises à jour de sondage, la modification des actions disponibles après une pression sur un bouton ou tout autre changement d’état asynchrone.

Le nouveau message n’a pas besoin de correspondre au type d’origine. Par exemple, si le message d’origine contient une pièce jointe, le nouveau message peut être un simple message texte.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `UpdateActivityAsync` activité existant à `TurnContext` la méthode de la classe. *Voir* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `updateActivity` activité existant à `TurnContext` la méthode de l’objet. *Voir* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

Pour mettre à jour un message existant, transmettez un nouvel `Activity` objet avec l’ID d' `update_activity` activité existant à `TurnContext` la méthode de la classe. Voir [TurnContextClass](link to Python API ref docs).

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a>Suppression de messages

Dans l’infrastructure bot, chaque message possède son propre identificateur d’activité unique.
Les messages peuvent être supprimés à l’aide de `DeleteActivity` la méthode de l’infrastructure bot, comme illustré ici.

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

Pour supprimer ce message, transmettez l’ID de cette activité `DeleteActivityAsync` à la méthode `TurnContext` de la classe. *Voir* la [méthode TurnContext. DeleteActivityAsync](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

Pour supprimer ce message, transmettez l’ID de cette activité `deleteActivity` à la méthode `TurnContext` de l’objet. *Voir* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

Pour supprimer ce message, transmettez l’ID de cette activité `delete_activity` à la méthode `TurnContext` de l’objet. Voir [Activity-Update-and-Delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---

