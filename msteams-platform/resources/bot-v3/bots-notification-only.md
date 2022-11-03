---
title: Bots avec notification seulement
description: Dans ce module, découvrez les bots de notification uniquement dans Microsoft Teams, le manifeste d’application et ses meilleures pratiques et limitations.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: ac412f37cba03c5da43163bf2eadd47adc676f08
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833015"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de notification uniquement dans Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si le seul objectif de votre bot est de remettre une notification aux utilisateurs et n’est pas conversationnel, vous pouvez activer le champ dans le `isNotificationOnly` manifeste de votre application. Cette action génère les modifications suivantes :

* Les utilisateurs ne peuvent pas envoyer un message à votre bot de notification uniquement.
* Les utilisateurs ne peuvent pas @mention le bot.

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

Les bots de notification uniquement utilisent la messagerie proactive pour communiquer avec l’utilisateur. Pour plus d’informations, consultez [Messagerie proactive pour les bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).
