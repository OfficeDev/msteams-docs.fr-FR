---
title: Bots avec notification seulement
description: Décrit les bots de notification uniquement qui sont dans Microsoft Teams
keywords: notification des bots teams
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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="24ffe-104">Bots de notification uniquement dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="24ffe-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="24ffe-105">Si l’unique objectif de votre bot est de remettre une notification aux utilisateurs et qu’il n’est pas conversationnel, vous pouvez activer le champ `isNotificationOnly` dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="24ffe-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="24ffe-106">Cela produit les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="24ffe-106">This produces the following changes:</span></span>

* <span data-ttu-id="24ffe-107">Les utilisateurs ne peuvent pas envoyer de message à votre bot de notification uniquement.</span><span class="sxs-lookup"><span data-stu-id="24ffe-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="24ffe-108">Les utilisateurs ne peuvent @mention le bot.</span><span class="sxs-lookup"><span data-stu-id="24ffe-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="24ffe-109">Les applications de bot uniquement s’surfacent dans le bac d’application personnel dans les deux cas : `isNotificationOnly: true` ou `isNotificationOnly: false` .</span><span class="sxs-lookup"><span data-stu-id="24ffe-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="24ffe-110">Manifeste d'application</span><span class="sxs-lookup"><span data-stu-id="24ffe-110">App manifest</span></span>

<span data-ttu-id="24ffe-111">Pour l’activer, définissez `isNotificationOnly` sur `true` .</span><span class="sxs-lookup"><span data-stu-id="24ffe-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="24ffe-112">N’ignorez pas que la valeur `isNotificationOnly` est boolén et non une chaîne.</span><span class="sxs-lookup"><span data-stu-id="24ffe-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="24ffe-113">Meilleures pratiques et limitations</span><span class="sxs-lookup"><span data-stu-id="24ffe-113">Best practices and limitations</span></span>

* <span data-ttu-id="24ffe-114">Les bots de notification uniquement utilisent une messagerie proactive pour communiquer avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="24ffe-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="24ffe-115">Pour plus d’informations, [consultez la messagerie proactive pour les bots.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)</span><span class="sxs-lookup"><span data-stu-id="24ffe-115">For more information, see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>
