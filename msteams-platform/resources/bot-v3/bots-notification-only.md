---
title: Bots avec notification seulement
description: Décrit les bots de notification uniquement dans Microsoft Teams
keywords: notification des bots teams
ms.topic: conceptual
ms.date: 01/29/2020
ms.openlocfilehash: 39ba25893623d6b963b44363b8458db6def58b60
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696072"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de notification uniquement dans Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si l'unique objectif de votre bot est de remettre une notification aux utilisateurs et qu'il n'est pas conversationnel, vous pouvez activer le champ `isNotificationOnly` dans le manifeste de votre application. Cela produit les modifications suivantes :

* Les utilisateurs ne peuvent pas envoyer de message à votre bot de notification uniquement.
* Les utilisateurs ne peuvent @mention le bot.

> [!NOTE]
> Les applications de bot uniquement s'surfacent dans le bac d'application personnel dans les deux cas : `isNotificationOnly: true` ou `isNotificationOnly: false` .

## <a name="app-manifest"></a>Manifeste de l'application

Pour l'activer, définissez `isNotificationOnly` sur `true` .

> [!NOTE]
> N'ignorez pas que la valeur `isNotificationOnly` est boolén et non une chaîne.

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

* Les bots de notification uniquement utilisent une messagerie proactive pour communiquer avec l'utilisateur. Pour [plus d'informations, voir](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) messagerie proactive pour les bots.
