---
title: Bots avec notification seulement
description: Décrit ce que les bots de notification seulement sont dans Microsoft Teams
keywords: équipes bots notification
ms.topic: conceptual
localization_priority: Normal
ms.date: 01/29/2020
ms.openlocfilehash: 3de462f73733f5f7cf223444ffe6deeb53faaaaa
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566760"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de notification uniquement dans Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si le seul but de votre bot est de fournir une notification aux utilisateurs et n’est pas conversationnel, vous pouvez activer le `isNotificationOnly` champ dans votre manifeste d’application. Ceci produit les changements suivants :

* Les utilisateurs ne peuvent pas envoyer un message à votre bot uniquement sur notification.
* Les utilisateurs ne peuvent @mention le bot.

> [!NOTE]
> Les applications bot-only feront surface dans le plateau d’application personnel dans les deux cas : `isNotificationOnly: true` ou `isNotificationOnly: false` .

## <a name="app-manifest"></a>Manifeste d'application

Pour activer cela, défini `isNotificationOnly` à `true` .

> [!NOTE]
> Sachez que la valeur de `isNotificationOnly` est boolean et non pas une chaîne.

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

* Les bots de notification uniquement utilisent la messagerie proactive pour communiquer avec l’utilisateur. Pour plus d’informations, consultez [la messagerie Proactive pour les bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).
