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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="b40ca-104">Robots de notifications uniquement dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="b40ca-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="b40ca-105">Si le seul objectif de votre robot est de fournir une notification aux utilisateurs et n’est pas conversationnel, vous pouvez `isNotificationOnly` activer le champ dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="b40ca-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="b40ca-106">Cela génère les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="b40ca-106">This produces the following changes:</span></span>

* <span data-ttu-id="b40ca-107">Les utilisateurs ne peuvent pas messageer votre robot de notification uniquement.</span><span class="sxs-lookup"><span data-stu-id="b40ca-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="b40ca-108">Les utilisateurs ne peuvent pas @mention le bot.</span><span class="sxs-lookup"><span data-stu-id="b40ca-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="b40ca-109">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="b40ca-109">App manifest</span></span>

<span data-ttu-id="b40ca-110">Pour activer ce paramètre, `isNotificationOnly` définissez `true`sur.</span><span class="sxs-lookup"><span data-stu-id="b40ca-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="b40ca-111">N’oubliez pas que la valeur `isNotificationOnly` de est booléenne et non une chaîne.</span><span class="sxs-lookup"><span data-stu-id="b40ca-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="b40ca-112">Meilleures pratiques et limitations</span><span class="sxs-lookup"><span data-stu-id="b40ca-112">Best practices and limitations</span></span>

* <span data-ttu-id="b40ca-113">Les robots de notification uniquement utilisent la messagerie proactive pour communiquer avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b40ca-113">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="b40ca-114">Pour plus d’informations, consultez la rubrique [messagerie proactive pour les robots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .</span><span class="sxs-lookup"><span data-stu-id="b40ca-114">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
