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
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="e76e7-104">Bots de notification uniquement dans Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="e76e7-104">Notification-only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="e76e7-105">Si le seul but de votre bot est de fournir une notification aux utilisateurs et n’est pas conversationnel, vous pouvez activer le `isNotificationOnly` champ dans votre manifeste d’application.</span><span class="sxs-lookup"><span data-stu-id="e76e7-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="e76e7-106">Ceci produit les changements suivants :</span><span class="sxs-lookup"><span data-stu-id="e76e7-106">This produces the following changes:</span></span>

* <span data-ttu-id="e76e7-107">Les utilisateurs ne peuvent pas envoyer un message à votre bot uniquement sur notification.</span><span class="sxs-lookup"><span data-stu-id="e76e7-107">Users cannot message your notification-only bot.</span></span>
* <span data-ttu-id="e76e7-108">Les utilisateurs ne peuvent @mention le bot.</span><span class="sxs-lookup"><span data-stu-id="e76e7-108">Users cannot @mention the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="e76e7-109">Les applications bot-only feront surface dans le plateau d’application personnel dans les deux cas : `isNotificationOnly: true` ou `isNotificationOnly: false` .</span><span class="sxs-lookup"><span data-stu-id="e76e7-109">The bot-only apps will surface in the personal app tray in both cases: `isNotificationOnly: true` or `isNotificationOnly: false`.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="e76e7-110">Manifeste d'application</span><span class="sxs-lookup"><span data-stu-id="e76e7-110">App manifest</span></span>

<span data-ttu-id="e76e7-111">Pour activer cela, défini `isNotificationOnly` à `true` .</span><span class="sxs-lookup"><span data-stu-id="e76e7-111">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="e76e7-112">Sachez que la valeur de `isNotificationOnly` est boolean et non pas une chaîne.</span><span class="sxs-lookup"><span data-stu-id="e76e7-112">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="e76e7-113">Meilleures pratiques et limitations</span><span class="sxs-lookup"><span data-stu-id="e76e7-113">Best practices and limitations</span></span>

* <span data-ttu-id="e76e7-114">Les bots de notification uniquement utilisent la messagerie proactive pour communiquer avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e76e7-114">Notification-only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="e76e7-115">Pour plus d’informations, consultez [la messagerie Proactive pour les bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span><span class="sxs-lookup"><span data-stu-id="e76e7-115">For more information, see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>
