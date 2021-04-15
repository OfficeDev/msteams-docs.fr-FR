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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="94a22-104">Bots de notification uniquement dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="94a22-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="94a22-105">Si l'unique objectif de votre bot est de remettre une notification aux utilisateurs et qu'il n'est pas conversationnel, vous pouvez activer le champ `isNotificationOnly` dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="94a22-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="94a22-106">Cela produit les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="94a22-106">This produces the following changes:</span></span>

* <span data-ttu-id="94a22-107">Les utilisateurs ne peuvent pas envoyer de message à votre bot de notification uniquement.</span><span class="sxs-lookup"><span data-stu-id="94a22-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="94a22-108">Les utilisateurs ne peuvent @mention le bot.</span><span class="sxs-lookup"><span data-stu-id="94a22-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="94a22-109">Les applications de bot uniquement s'surfacent dans le bac d'application personnel dans les deux cas : `isNotificationOnly: true` ou `isNotificationOnly: false` .</span><span class="sxs-lookup"><span data-stu-id="94a22-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="94a22-110">Manifeste de l'application</span><span class="sxs-lookup"><span data-stu-id="94a22-110">App manifest</span></span>

<span data-ttu-id="94a22-111">Pour l'activer, définissez `isNotificationOnly` sur `true` .</span><span class="sxs-lookup"><span data-stu-id="94a22-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="94a22-112">N'ignorez pas que la valeur `isNotificationOnly` est boolén et non une chaîne.</span><span class="sxs-lookup"><span data-stu-id="94a22-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="94a22-113">Meilleures pratiques et limitations</span><span class="sxs-lookup"><span data-stu-id="94a22-113">Best practices and limitations</span></span>

* <span data-ttu-id="94a22-114">Les bots de notification uniquement utilisent une messagerie proactive pour communiquer avec l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="94a22-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="94a22-115">Pour [plus d'informations, voir](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) messagerie proactive pour les bots.</span><span class="sxs-lookup"><span data-stu-id="94a22-115">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
