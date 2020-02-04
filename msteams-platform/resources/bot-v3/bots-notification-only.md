---
title: Robots de notification uniquement
description: Décrit les robots de notification uniquement pour Microsoft Teams.
keywords: notification des bots de teams
ms.date: 05/20/2019
ms.openlocfilehash: 37652bc2d6171191c81be4e5a2875f47c79574f9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673575"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Robots de notifications uniquement dans Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si le seul objectif de votre robot est de fournir une notification aux utilisateurs et n’est pas conversationnel, vous pouvez `isNotificationOnly` activer le champ dans le manifeste de votre application. Cela génère les modifications suivantes :

* Les utilisateurs ne peuvent pas messageer votre seul bot de notification.
* Les utilisateurs ne peuvent pas @mention le bot.

## <a name="app-manifest"></a>Manifeste de l’application

Pour activer ce paramètre, `isNotificationOnly` définissez `true`sur.

> [!NOTE]
> N’oubliez pas que la valeur `isNotificationOnly` de est booléenne et non une chaîne.

```json
{
  ⋮
  "bots":[
    {
      "botId":"[Microsoft App ID for your bot]",
      "isNotificationOnly": true,
      "scopes": [
        "personal",
        "team"
      ],
    }
  ],
  ...
}
```

## <a name="best-practices-and-limitations"></a>Meilleures pratiques et limitations

* Vous ne pouvez pas `personal` créer une notification d’étendue uniquement bot, car l’utilisateur ne peut pas messageer votre notification de robot uniquement dans une conversation personnelle. Cela signifie que vous ne pouvez pas `conversationUpdate` recevoir un événement qui vous fournira les informations nécessaires pour envoyer une notification. Votre robot de notification ne fonctionnera correctement que s’il prend `team` en charge l’étendue et est ajouté à une équipe. Dans le paramètre d’équipe, votre bot aura accès aux informations nécessaires pour envoyer une notification à un canal ou à un utilisateur de manière privée.
* Notification uniquement les robots utilisent la messagerie proactive pour communiquer avec l’utilisateur. Pour plus d’informations, consultez la rubrique [messagerie proactive pour les robots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .
