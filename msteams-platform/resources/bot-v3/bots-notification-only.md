---
title: Robots de notification uniquement
description: Décrit les robots de notification uniquement pour Microsoft Teams.
keywords: notification des bots de teams
ms.date: 05/20/2019
ms.openlocfilehash: 37652bc2d6171191c81be4e5a2875f47c79574f9
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673575"
---
# <a name="notification-only-bots-in-microsoft-teams"></a><span data-ttu-id="37467-104">Robots de notifications uniquement dans Microsoft teams</span><span class="sxs-lookup"><span data-stu-id="37467-104">Notification only bots in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="37467-105">Si le seul objectif de votre robot est de fournir une notification aux utilisateurs et n’est pas conversationnel, vous pouvez `isNotificationOnly` activer le champ dans le manifeste de votre application.</span><span class="sxs-lookup"><span data-stu-id="37467-105">If your bot's sole purpose is to deliver notification to users and is not conversational, you can enable the `isNotificationOnly` field in your app manifest.</span></span> <span data-ttu-id="37467-106">Cela génère les modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="37467-106">This produces the following changes:</span></span>

* <span data-ttu-id="37467-107">Les utilisateurs ne peuvent pas messageer votre seul bot de notification.</span><span class="sxs-lookup"><span data-stu-id="37467-107">Users cannot message your notification only bot.</span></span>
* <span data-ttu-id="37467-108">Les utilisateurs ne peuvent pas @mention le bot.</span><span class="sxs-lookup"><span data-stu-id="37467-108">Users cannot @mention the bot.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="37467-109">Manifeste de l’application</span><span class="sxs-lookup"><span data-stu-id="37467-109">App manifest</span></span>

<span data-ttu-id="37467-110">Pour activer ce paramètre, `isNotificationOnly` définissez `true`sur.</span><span class="sxs-lookup"><span data-stu-id="37467-110">To enable this, set `isNotificationOnly` to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="37467-111">N’oubliez pas que la valeur `isNotificationOnly` de est booléenne et non une chaîne.</span><span class="sxs-lookup"><span data-stu-id="37467-111">Be aware that the value of `isNotificationOnly` is boolean and not a string.</span></span>

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

## <a name="best-practices-and-limitations"></a><span data-ttu-id="37467-112">Meilleures pratiques et limitations</span><span class="sxs-lookup"><span data-stu-id="37467-112">Best practices and limitations</span></span>

* <span data-ttu-id="37467-113">Vous ne pouvez pas `personal` créer une notification d’étendue uniquement bot, car l’utilisateur ne peut pas messageer votre notification de robot uniquement dans une conversation personnelle.</span><span class="sxs-lookup"><span data-stu-id="37467-113">You cannot create a `personal` scoped notification only bot, as the user cannot message your notification only bot in a personal chat.</span></span> <span data-ttu-id="37467-114">Cela signifie que vous ne pouvez pas `conversationUpdate` recevoir un événement qui vous fournira les informations nécessaires pour envoyer une notification.</span><span class="sxs-lookup"><span data-stu-id="37467-114">This means that you can't receive a `conversationUpdate` event that would provide you with the necessary details to send a notification.</span></span> <span data-ttu-id="37467-115">Votre robot de notification ne fonctionnera correctement que s’il prend `team` en charge l’étendue et est ajouté à une équipe.</span><span class="sxs-lookup"><span data-stu-id="37467-115">Your notification only bot will only function correctly if it supports the `team` scope and is added to a team.</span></span> <span data-ttu-id="37467-116">Dans le paramètre d’équipe, votre bot aura accès aux informations nécessaires pour envoyer une notification à un canal ou à un utilisateur de manière privée.</span><span class="sxs-lookup"><span data-stu-id="37467-116">In the team setting, your bot will have access to the necessary information to either send a notification to a channel or privately to a user.</span></span>
* <span data-ttu-id="37467-117">Notification uniquement les robots utilisent la messagerie proactive pour communiquer avec l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="37467-117">Notification only bots use proactive messaging to communicate with the user.</span></span> <span data-ttu-id="37467-118">Pour plus d’informations, consultez la rubrique [messagerie proactive pour les robots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) .</span><span class="sxs-lookup"><span data-stu-id="37467-118">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more details.</span></span>
