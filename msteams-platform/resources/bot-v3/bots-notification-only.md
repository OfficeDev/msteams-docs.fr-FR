---
title: Bots avec notification seulement
description: Décrit les bots de notification uniquement qui sont dans Microsoft Teams
keywords: notification des bots teams
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 01/29/2020
ms.openlocfilehash: d3ee5343ea159950859237f2a488557d9063eb6e
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355726"
---
# <a name="notification-only-bots-in-microsoft-teams"></a>Bots de notification uniquement dans Microsoft Teams

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Si l’unique objectif de votre bot est de remettre une notification aux utilisateurs et qu’il n’est pas conversationnel, `isNotificationOnly` vous pouvez activer le champ dans le manifeste de votre application. Cela produit les modifications suivantes :

* Les utilisateurs ne peuvent pas envoyer de message à votre bot de notification uniquement.
* Les utilisateurs ne peuvent @mention le bot.

> [!NOTE]
> Les applications de bot uniquement s’surfacent dans le bac d’application personnel dans les deux cas : `isNotificationOnly: true` ou `isNotificationOnly: false`.

## <a name="app-manifest"></a>Manifeste d'application

Pour l’activer, définissez sur `isNotificationOnly` `true`.

> [!NOTE]
> La valeur est `isNotificationOnly` Boolean et non une chaîne.

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

* Les bots de notification uniquement utilisent une messagerie proactive pour communiquer avec l’utilisateur. Pour plus d’informations, voir [Messagerie proactive pour les bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).
