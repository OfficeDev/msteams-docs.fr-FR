---
title: Bots avec notification seulement
description: Décrit les bots de notification uniquement dans Microsoft Teams
keywords: notification des bots teams
ms.topic: conceptual
ms.localizationpriority: high
ms.date: 01/29/2020
ms.openlocfilehash: 1ee009fb76a52bcebdd3fe24c7a672f1ed455b42
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111478"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de notification uniquement dans Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si le seul objectif de votre bot est de remettre une notification aux utilisateurs et qu’il n’est pas conversationnel, vous pouvez activer le champ `isNotificationOnly` dans le manifeste de votre application. Cette action génère les modifications suivantes :

* Les utilisateurs ne peuvent pas envoyer de message à votre bot de notification uniquement.
* Les utilisateurs ne peuvent pas @mentionner le bot.

> [!NOTE]
> Les bots de notification uniquement apparaissent dans la barre d’état des applications personnelles dans les deux cas : `isNotificationOnly: true` ou `isNotificationOnly: false`.

## <a name="app-manifest"></a>Manifeste d'application

Pour activer cette option, définissez `isNotificationOnly` sur `true`.

> [!NOTE]
> La valeur est `isNotificationOnly` booléenne et non une chaîne.

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

* Les bots de notification uniquement utilisent la messagerie proactive pour communiquer avec l’utilisateur. Pour plus d’informations, consultez [Messagerie proactive pour les bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).
