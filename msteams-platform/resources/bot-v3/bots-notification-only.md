---
title: Robots de notification uniquement
description: Décrit les robots de notification uniquement dans Microsoft teams
keywords: notification des bots de teams
ms.date: 01/29/2020
ms.openlocfilehash: d312f9cd4558d35fc2492b5cf0b4f77b65660833
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783905"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Robots de notifications uniquement dans Microsoft teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si le seul objectif de votre robot est de fournir une notification aux utilisateurs et n’est pas conversationnel, vous pouvez `isNotificationOnly` activer le champ dans le manifeste de votre application. Cela génère les modifications suivantes :

* Les utilisateurs ne peuvent pas messageer votre robot de notification uniquement.
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

* Les robots de notification uniquement utilisent la messagerie proactive pour communiquer avec l’utilisateur. Pour plus d’informations, consultez la rubrique [messagerie proactive pour les robots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .
